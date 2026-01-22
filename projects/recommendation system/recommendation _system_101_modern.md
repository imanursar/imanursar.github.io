---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Modern Recommendation System Framework
parent: Recommendation System
permalink: /recommendation system/rec_sys_modern
nav_order: 101
---

# Modern Recommendation System Framework

Recommendation
{: .badge .badge-pill .badge-primary }
Optimization
{: .badge .badge-pill .badge-secondary }
matchmaking
{: .badge .badge-pill .badge-info }

These systems typically involve **documents** (entities a system recommends, like movies or videos), **queries** (information needed to make recommendations, such as user data or location), and **embeddings** (mappings of queries or documents to a vector space called embedding space).

Below is a common architecture for a recommendation system model:

<img src="/assets/images/recommendation/rs_101/rs_101_06.webp" alt="drawing"/>

- **Candidate Generation**: starting with a vast corpus and generating a smaller subset of candidates. 
- **Scoring**: the model ranks the candidates to select a smaller, more refined set of documents. 
- **Re-ranking**: This final step refines the recommendations. 

### Funnel Architecture
Many large-scale recommendation systems implement these processes in two main stages: retrieval and ranking that wrap up in funnel architecture. Funnel architectures are designed to progressively refine a vast pool of potential candidates into a smaller, more relevant set of recommendations through multiple stages. in example:
- Eugene Yan’s 2-Stage (2x2) Model of a Recommender System
- Nvidia’s 4-Stage (2x4) Model of a Recommender System

<img src="/assets/images/recommendation/rs_101/rs_101_07.webp" alt="drawing"/>

### 2-Stage (2x2) Recommender Systems
The 2-Stage (2x2) model involves two main stages:
  - **Retrieval**: Quickly narrows down the vast candidate pool (e.g., millions of items) to a smaller subset using scalable models such as matrix factorization or two-tower architectures.
  - **Ranking**: Applies sophisticated models incorporating richer feature sets, such as user context or item-specific details, to assign relevance scores and generate a personalized, ranked list.

<img src="/assets/images/recommendation/rs_101/rs_101_08.webp" alt="drawing"/>

Eugene Yan’s 2x2 model identifies two main dimensions within discovery systems:
  - Environment: Offline (flows bottom-up) vs. Online (left-to-right).
  - Process: Candidate Retrieval vs. Ranking.

With offline environment, batch processes handle tasks such as model training, creating embeddings for catalog items, and developing structures like approximate nearest neighbors (ANN) indices or knowledge graphs to identify item similarity. The offline stage may also involve loading item and user data into a feature store, which helps augment input data during ranking.

Meanwhile, The online environment serves individual user requests in real-time, utilizing artifacts generated offline (e.g., ANN indices, knowledge graphs, models).

[source](https://eugeneyan.com/writing/system-design-for-discovery/)

### 4-Stage (2x4) Recommender Systems

<img src="/assets/images/recommendation/rs_101/rs_101_09.webp" alt="drawing"/>

The 4-Stage (2x4) model extends the 2x2 framework with two intermediary stages for greater precision and flexibility:

  - **Retrieval**: Identifies an initial set of candidates, emphasizing efficiency and broad coverage. Using methods such as matrix factorization, two-tower models, or ANN. Retrieval is computationally efficient, ensuring the model can quickly handle a large number of items and narrow them down to a set of potential candidates for scoring.
  - **Filtering**: Applies business rules to exclude ineligible or irrelevant items (e.g., out-of-stock products inappropriate for the user, or regionally restricted content). Filtering ensures that the system does not rely on retrieval or scoring models to handle business-specific logic, allowing for more precise control over item eligibility.
  - **Scoring**: Involves a detailed analysis of the remaining candidates,using models that factor in additional features (e.g., user data, user-item interactions, contextual information) to predict user interest. Scoring can leverage sophisticated models, such as deep learning architectures, to assign interaction likelihoods (e.g., click, purchase probability) to each candidate.
  - **Ranking (or Ordering)**: The system arranges items into an ordered list for the user. Although scoring assigns relevance scores to each item, the ordering stage allows further adjustments to ensure a diverse mix of recommendations or to meet additional criteria like novelty and business goals.

<img src="/assets/images/recommendation/rs_101/rs_101_10.webp" alt="drawing"/>

[source](https://medium.com/nvidia-merlin/recommender-systems-not-just-recommender-models-485c161c755e)

These frameworks allow recommender systems to balance computational efficiency in early stages with precision and personalization in later stages. They are widely used in large-scale systems like Netflix, YouTube, and Amazon.

---

## Candidate Generation

- Candidate generation is the first stage of recommendations and is typically achieved by finding features for users that relate to features of the items. 
- This step is the process of **selecting a set of items that are likely to be recommended to a user**. This process is typically performed after user preferences have been collected, and it involves filtering a large set of potential recommendations down to a more manageable number.
- **Given a query (user information), the model generates a set of relevant candidates (videos, movies)**.
- In Example: User searches for computer at some location. It would filter out searches that were not in user's location and look at latent representation of the user and find items that have latent representations that are close using approximate nearest neighbor algorithms.
- **Candidate generation is for recommender systems like a search engine where the candidates are not particularly based on time. whereas candidate retrieval is for news-feed based systems where time is important.**

### The goal of candidate generation:
- To reduce the number of items that must be evaluated by the system.
- Still ensuring that the most relevant recommendations are included.

### Two common candidate generation approaches: 
- Content-based filtering: Uses similarity between content to recommend new content. 
- Collaborative filtering: Uses similarity between queries (2 or more users) and items (videos, movies) to provide recommendations. 