---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Evaluation
parent: Recommendation System
permalink: /recommendation system/evaluation
nav_order: 105
toc: true
---

# Evaluation

Recommendation
{: .badge .badge-pill .badge-primary }
Optimization
{: .badge .badge-pill .badge-secondary }
matchmaking
{: .badge .badge-pill .badge-info }

* Do not remove this line (it will not be displayed)
{:toc}

In ranked systems like search engines, users typically look only at the first few results. Even if a system returns many relevant items further down the list, they are unlikely to be seen or clicked. Thus, the term `@K` is suitable for evaluation our model with focusing on first result.

## Evaluation Metric
### **Normalized Discounted Cumulative Gain (NDCG)**
  - Is a list-wise ranking metric used to evaluate the quality of a recommender system’s ranked list of recommendations.
  - It compares rankings to an ideal order where all relevant items are at the top of the list.
  - A relevance score is a ground truth or target value necessary for evaluating ranking system quality. It can be a binary label (relevant or not / the user clicked on, watched, or purchased an item or not) or a numerical score (e.g., 1 to 5 / where different weights are assigned to specific user actions, reflecting a relative degree of match).
  - K-parameter is a user-assigned parameter that defines the cutoff point (list length) while evaluating ranking quality. For example, you can only look at top-10 items.
  - A gain of a single recommended item is its relevance score, be it binary or graded.
  - Cumulative gain is a measure of the total relevance of the ranked list. It sums up the relevance scores of the individual items in the list.
  - A logarithmic discount gain (DCG) helps assign lower gain when relevant items appear further down in the ranked list (logarithmic penalty).
  - DCG; The principle is to position-discount the retrieved items and assign higher weights to relevant items that appear at the top of the list, reflecting the intuition that users are more likely to interact with items presented earlier.
  - IDCG represents the maximum achievable DCG with the same set of relevance scores but in the perfect ranking order. 
  - **ELI5** 
    > “Did we rank the most valuable items at the top?”
  - **Formula and Example**:
    - Define Relevance Scale (NDCG requires graded relevance to show its full value)
      - Purchase = 3
      - Add-to-cart = 2
      - View = 1
      - no interaction = 0
    - Get model's top-k Recommendation list

      | Rank (i) | Item | User Action    | Relevance (relᵢ) |
      | -------- | ---- | -------------- | ---------------- |
      | 1        | A    | Purchased      | 3                |
      | 2        | B    | Viewed         | 1                |
      | 3        | C    | No interaction | 0                |
      | 4        | D    | Add-to-cart    | 2                |
      | 5        | E    | No interaction | 0                |

    - Discounted Cumulative Gain (DCG@k): `DCG@K = Σ (relᵢ / log₂(i + 1)) , for i = 1..K`

      | Rank (i) | relᵢ | log₂(i+1)       | relᵢ / log₂(i+1) |
      | -------- | ---- | --------------- | ---------------- |
      | 1        | 3    | log₂(2) = 1.000 | 3.000            |
      | 2        | 1    | log₂(3) ≈ 1.585 | 0.631            |
      | 3        | 0    | log₂(4) = 2.000 | 0.000            |
      | 4        | 2    | log₂(5) ≈ 2.322 | 0.861            |
      | 5        | 0    | log₂(6) ≈ 2.585 | 0.000            |

      ```math
        DCG@5 = 3.000 + 0.631 + 0.000 + 0.861 + 0.000 = 4.492
      ```
    - Construct the Ideal Ranking (IDCG@5), Sort the same items by true relevance, highest first.

      | Ideal Rank | Item | Relevance |
      | ---------- | ---- | --------- |
      | 1          | A    | 3         |
      | 2          | D    | 2         |
      | 3          | B    | 1         |
      | 4          | C    | 0         |
      | 5          | E    | 0         |

    - Compute IDCG@5

      | Rank | relᵢ | log₂(i+1) | relᵢ / log₂(i+1) |
      | ---- | ---- | --------- | ---------------- |
      | 1    | 3    | 1.000     | 3.000            |
      | 2    | 2    | 1.585     | 1.262            |
      | 3    | 1    | 2.000     | 0.500            |
      | 4    | 0    | 2.322     | 0.000            |
      | 5    | 0    | 2.585     | 0.000            |

      ```math
        IDCG@5 = 3.000 + 1.262 + 0.500 = 4.762
      ```
    - Compute NDCG@5
      
      ```math
        NDCG@5  = DCG@5 / IDCG@5
                = 4.492 / 4.762
                ≈ 0.943
      ```
    - result `0 ≤ NDCG@K ≤ 1`
  - **Goals**:
    - Correct items
    - Correct order
    - Higher positions more than lower ones (Items at rank 1 matter more than rank 10)
    - Purchase > cart > view (graded relevance)
    - using `log₂(i+1)` Discount could give us; Rank 1 is ~3× more valuable than rank 10 and matches user attention patterns.
  - **Limitation**:
    - Revelance scales must be consistent across models
    - Users with no relevant items, define NDCG = 0 or exclude consistently
    - The absolute values of DCG depend on the number of items in the list and the relevance scores assigned.
  - [sources](https://www.evidentlyai.com/ranking-metrics/ndcg-metric#discounted-gain-dcg) 
### **Recall@K**
  - **ELI5** 
    > “Of all items the user would actually interact with, how many did we successfully put into the top K recommendations?”
  - **Formula**: `Recall@K = (# relevant items in top K) / (total # relevant items)`
  - elevant items = items the user actually purchased / clicked in the evaluation window.
  - **Example**:
    - user relevant = {A, B, C, D}
    - model's top-5 = {A, X, Y, C, Z}
    - Relevant in top-5 = {A, C} = 2 items
    - Recall@5 = 2 / 4 = 0.50
  - **Goals**:
    - Measures coverage of user intent
    - Answers: “Did we miss something the user wanted?”
    - Critical when:
      - You have multiple relevant items per user
      - You care about not missing purchases
  - **Limitation**:
    - Does not care about ranking order
    - Item at position #1 and #K are treated equally
### **Precision@k**
  - is defined as the proportion of recommended items within the top-k set that are relevant.
  - **ELI5** 
    > “Of all items the user would actually interact with, how many are relevant?”
  - **Formula**: `Precision@K = (# relevant items in top K) / K`
### **Mean Reciprocal Rank (MRR)**
  - MRR is calculated by taking the reciprocal of the rank of the first relevant item and averaging these reciprocal ranks across multiple queries or instances.
  - MRR is very simple to explain. It provides a straightforward measure of how quickly you find a relevant item in the list.
  - MRR considers only the position of the first relevant item in the list. It does not care what happens after it.
  - MRR can only handle binary relevance scores and treats the items as either relevant or not.
  - MRR aligns well with scenarios where the primary goal is to present the most relevant item as early as possible or when there is a single most relevant and correct answer. 
  - This metric is quite intuitive: MRR reflects how soon, on average, we can find a relevant item for each user within the first K positions. It emphasizes the importance of being correct early in the list.
  - A Reciprocal Rank is the inverse of the position of the first relevant item. If the first relevant item is in position 2, the reciprocal rank is 1/2. 
  - **Formula**
    - `MRR = 1/U Σ 1/rank_i`
    - U is the total number of users (in case of recommendations) or queries (in case of information retrieval) in the evaluated dataset.
    - rank_i is the position of the first relevant item for user u in the top-K results.
  - This parameter calculate sum only the first relevant item for each user and divide with all users number.
  - **Example**
    - User 1: The relevant result appears in the 3rd position, Reciprocal Rank: 1/3.
    - User 2: The first relevant result appears in the 1st position, Reciprocal Rank: 1.
    - User 3: The relevant result appears in the 3rd position, Reciprocal Rank: 1/3.
    - User 4: All results are non-relevant, Reciprocal Rank: 0.
    - MRR = (1/3 + 1 + 1/3 + 0) / 4 = 0.417
  - **Advantage**
    - MRR is excellent for scenarios with a single correct answer.
    - MRR is easily interpretable
    - MRR disregards the relevance of items beyond the first one
### **Average Reciprocal Hit Rate (ARHR)**
  - is a generalization of MRR for scenarios involving multiple clicked items, and it is often used interchangeably with MRR in the literature.
  - The Reciprocal Hit Rate (RHR) is computed for each user by summing the reciprocals of the positions of the clicked items within the recommendation list. For instance, if the third item in the list is clicked, its reciprocal would be 1/3. The RHR for a user is the sum of these reciprocals for all clicked items.
  - Similar to MRR, a higher ARHR indicates that the recommender system is more effective in prominently presenting relevant items, leading to enhanced user engagement and satisfaction.
  - ARHR is based on the top k positions in the ranked list. The metric emphasizes the importance of relevant items appearing within these top k results, reflecting the system’s ability to present the most relevant results quickly.
### **Mean Average Precision at k (mAP@k)**
  - Calculate and average the Precision (the share of relevant items up to a given position) at each relevant position in top K.
  - MAP is designed to evaluate a ranking or recommender system with a binary relevance function.
  - MAP gives more weight to the relevant items at the top of the list. Since the metric is based on Precision values at each relevant position in the ranked list, it is more sensitive to changes in the early positions.
  - MAP bias towards the top ranks, it is often suitable when the emphasis is on Precision at higher ranks.
  - By considering both the average precision across cutoff points and the mean precision across users, mAP provides an aggregated measure of the recommender system’s performance, capturing its ability to recommend relevant items at various positions within the list and offering a comprehensive evaluation across the entire user population.
  - **Formula**
    - `Precision@K = (# relevant items in top K) / (K)`
    - `AP@K = 1/N Σ Precision@K x rel@K`
    - `MAP@K = 1/U Σ AP@K`
    - N is the total number of relevant items for a particular user.
    - rel(k) equals 1 if the item at position k is relevant and 0 otherwise.
    - K is a chosen cutoff point.
    - U is the total number of users or queries (in information retrieval) in the evaluated dataset.
    - for AP@K we calculate each order with its relevant position / its actual position.
    - AP is the average Precision for a given ranking list. 
    - Compute Precision@K 

      | Rank | rel | Precision@K  |
      | ---- | ---- | --------- |
      | 1    | 1    | 1/1 = 1 x 0    |
      | 2    | 0    | 1/2 = 0.5 x 1  |
      | 3    | 0    | 1/3 = 0.33 x 0 |
      | 4    | 1    | 2/4 = 0.5 x 1  |
      | 5    | 1    | 3/5 = 0.6 x 1  |
      | 6    | 0    | 3/6 = 0.5 x 0  |

    - Compute `AP@6 = (1 + 0.5 + 0.6) / 3 = 0.7`
  - From Precision@K and Recall@K we could generate Precision-Recall curve. It plots the Precision values against different Recall values at each K. This helps you visualize the step changes as you move down the ranked list. Then, you can think of Average Precision as the interpolated area under the Precision-Recall curve.
  - **Advantage**
    - MAP is its sensitivity to rank.
    - Focus on getting the top results right.
  - **Limitation**
    - Limited interpretability.
### **Mean Average Recall at k (mAR@k)**
  - Calculate and average the Recall (the share of relevant items up to a given position) at each relevant position in top K.
  - By integrating both the average recall across cutoff points and the mean recall across users, mAR provides a holistic measure of the system’s performance, capturing its ability to recommend a diverse range of relevant items at various positions within the list and offering a comprehensive evaluation across all users.
  - **Formula**
    - `Recall@K = (# relevant items in top K) / (total # relevant items)`
    - `AR@K = 1/N Σ Recall@K x rel@K`
    - `MAR@K = 1/U Σ AP@K`
### **Fraction of Concordant Pairs (FCP)**
  - is a ranking metric that evaluates how well the recommender system orders items in alignment with user preferences.
  - **FCP focuses on the pairwise correctness of rankings** and provides a measure of ranking quality by comparing the relative positions of items.
  - **Formula**: `FCP = Number of Concordant Pairs / (Number of Concordant Pairs + Number of Disconcordant Pairs)`
    - Concordant Pair: A pair (i,j) is concordant if:
      - The user prefers item i over item j (e.g., based on clicks, ratings, or other implicit/explicit feedback)
      - The system ranks i higher than j.
    - Discordant Pair: A pair (i,j) is discordant if:
      - The user prefers item i over item j, but the system ranks j higher than i.
    - Example:
      - User true preferences being A>B>C. The system ranks them as B,A,C.
      - Concordant Pairs: A>C (System ranks A above C, which matches user preference).
      - Discordant Pairs:
        - A>B (System ranks B above A).
        - B>C (System ranks C above B).
      - FCP Calculation:
        - Concordant Pairs: 1, Discordant Pairs: 2. FCP=1/(1+2)=0.33.
  - **Advantages**
    - FCP evaluates the ranking quality at the level of item pairs, making it particularly suited for systems where relative preferences between items are important.
    - Interpretability: The metric is easy to interpret, as it directly quantifies the proportion of pairs ranked correctly.
    - Granularity: By focusing on pairwise comparisons
    - Preference Alignment: It provides a direct measure of how well the system’s rankings reflect user preferences.
  - **Limitations**
    - Computational Cost: due to the quadratic growth in the number of item pairs as the dataset size increases.
    - Data Dependency: FCP relies on having well-defined user preferences for pairs of items, which may not always be readily available.


## Precision@k vs Recall@K
  - Precision@k is often preferred in these cases because it focuses specifically on the top-k results that users actually engage with.
  - Precision@k is especially well-suited to scenarios where top results must be highly accurate—such as e-commerce recommendations, news feeds, or image search.
  - Pure Recall is best when: Missing any relevant item is equally important (e.g., medical document retrieval, legal discovery).
  - Recall@k helps assess whether relevant items are present within the top results that users are most likely to engage with.
  - While **Recall@k focuses on whether a system includes relevant items** within the top-k results, **it does not penalize irrelevant ones**. This makes it **useful for evaluating coverage, but not quality**.
  - While **Precision@k focuses on the cost of showing irrelevant results** or where **users care more about the precision of what they see** than how many total relevant items are found.
  - Precision@k doesn’t depend on knowing the total number of relevant items in the dataset. This makes it especially useful in open-ended or real-time systems where the full set of relevant results is unknown.
  - Precision@k is preferred when relevance at the top matters more than completeness. A high precision means most of the top-k results are actually useful, which improves user trust and satisfaction.
  - Precision@k is particularly valuable in applications like:
    - News or content recommendation (users only see a handful of articles or videos).
    - Product search (top results must match user intent precisely).
    - Spam detection or filtering systems (false positives are harmful).
  - Sensitivity to k in Precision@k: Precision@k is sensitive to the choice of k. If k is too small, the metric may not capture broader performance trends. If k is too large, precision can be artificially lowered by including less relevant items that no user would ever scroll down to. Furthermore, the metric assumes all positions within the top-k are equally important, which may not reflect actual user behavior or expectations.
  - Recall implicitly assumes that retrieving more relevant items is always better. But in many real-world systems, users don’t want more—they want better. For instance, a user looking for a specific news article or shopping item typically wants just one or two good results, not every possible match.


## Choosing Between Precision and Recall @ k, MRR, ARHR, MAP, or NDCG
  Several key considerations must be evaluated based on the nature of the data and the specific objectives of the recommendation system:
  - **Precision and Recall @k**:
    - Focus: These metrics are particularly useful when you are interested in the performance of the system within a specific cutoff point k.
    - Suitability: These metrics are straightforward and useful in scenarios where the user typically reviews only a limited number of recommendations and relevance is binary.
    - Limitation: The precision and recall @ k metrics measures how precise the output lists are, but they are not an indicator of ranking quality.
  - **Fraction of Concordant Pairs (FCP)**:
    - Focus: FCP measures the pairwise ranking accuracy of a recommendation system by evaluating how well the system’s ranking aligns with the user’s preferences for item pairs.
    - Suitability: FCP is ideal for systems where the correctness of relative rankings between item pairs is critical.
    - Limitation: FCP can be computationally expensive for large datasets because the number of item pairs grows quadratically with the size of the dataset.
  - **Mean Reciprocal Rank (MRR)**:
    - Focus: MRR is based on the rank of the first relevant item in the list, making it particularly useful when the system is expected to retrieve a single relevant item or when the user’s primary interest is finding the first relevant result quickly.
    - Suitability: MRR is well-suited for systems like search engines or question-answering platforms where the goal is to return the first relevant item as quickly as possible.
    - Limitation: In an event recommendation system where multiple relevant events may be of interest to the user, MRR is not an ideal choice. 
  - **Average Reciprocal Hit Rate (ARHR)**:
    - Focus: ARHR is an extension of MRR that accounts for all relevant items within the top k positions. ARHR calculates the reciprocal of the rank for each relevant item found within the top k positions and averages them.
    - Suitability: ARHR is suitable for recommendation systems where it is important not only to retrieve the first relevant item quickly but also to ensure that all relevant items are ranked as high as possible within the top k positions.
    - Limitation: Like MRR, ARHR is sensitive to the position of relevant items, but it still may not fully capture the quality of the overall ranking beyond the top k positions.
  - **Mean Average Precision (mAP):**
    - Focus: mAP is a metric that calculates the average precision across multiple queries, taking into account the ranking of all relevant items. It is designed for binary relevance, where each item is either relevant or not.
    - Suitability: mAP is particularly well-suited for systems where relevance is binary, such as event recommendation systems, where an event is either relevant (e.g., a user registered) or irrelevant (e.g., a user did not register).
    - Limitation: Unlike Precision or Recall at k, mAP does measure ranking quality (since the AP score is high if more relevant items are located at the top of the list).
  - **Normalized Discounted Cumulative Gain (NDCG)**:
    - Focus: NDCG measures the quality of a ranking by evaluating how well the most relevant items are ranked near the top of the list.
    - Suitability: NDCG is a strong choice when the relevance score between a user and an item is non-binary.
    - Limitation: NDCG may not be the best fit in scenarios where relevance is strictly binary (either relevant or not).


## Evaluating Re-ranking
  Diversity, novelty/freshness, and serendipity are valuable metrics for evaluating re-ranking in recommender systems. These metrics go beyond traditional accuracy-focused measures (like precision, recall for candidate retrieval or NDCG for ranking) to provide a more holistic evaluation of how well a recommender system meets user needs and enhances user experience. 
  - **Diversity**:
    - Diversity measures the degree to which recommended items cover different aspects of the user’s preferences, ensuring that the recommendations are varied rather than repetitive.
    - How to Measure: computing the average pairwise dissimilarity between the recommended items. we can use a cosine similarity measure between item pairs.
    - Formula: cosine similarity(i,j) = count(users with i and j) / (count(users with i)^1/2) x (count(users with j)^1/2)