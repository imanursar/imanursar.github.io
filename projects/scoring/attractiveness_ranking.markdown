---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Attractiveness Ranking (MCDA & EWM)
parent: Scoring
permalink: /Scoring/arractiveness_ranking
nav_order: 103
---

# Attractiveness Ranking (MCDA & EWM)

scoring
{: .badge .badge-pill .badge-primary }
attractiveness
{: .badge .badge-pill .badge-secondary }
ranking
{: .badge .badge-pill .badge-info }

* Do not remove this line (it will not be displayed)
{:toc}

# Problem

Imagine your family wants to decide where to go on vacation.
There are 5 cities.

| City | Beach | Food  | Cost | Safety | Attractions |
| ---- | ----- | ----- | ---- | ------ | ----------- |
| A    | ⭐⭐⭐⭐⭐ | ⭐⭐⭐   | $$   | High   | Many        |
| B    | ⭐⭐    | ⭐⭐⭐⭐⭐ | $    | Medium | Many        |
| C    | ⭐⭐⭐⭐  | ⭐⭐⭐⭐  | $$$  | High   | Moderate    |

Everyone has different opinions. How do you fairly decide which city is the "best"? One way is to give every factor a score and combine them. This is exactly what **Multi-Criteria Decision Analysis (MCDA)** does.

Suppose every city has almost identical safety that range from 90-95 in safety value. But every city has attractions with huge differences in attractions 10-100. This criterion tells us much more. So maybe Attractions should receive a larger weight than Safety. That idea is exactly what the **Entropy Weight Method (EWM)** does.

Instead of a human saying
> "Safety = 30%"

the data itself says
> "Safety doesn't vary much, so it shouldn't influence ranking much."

while
> "Tourism attractions vary a lot, so give them more importance."

# What is Attractiveness Ranking?

With some points/objects and multiple parameters, attractiveness isn't measured by one number and it depends on many indicators.

For Example, in business decision, how to decide which points or areas is more attractive compare to other based on:
- GDP
- Average income
- Investment
- Employment
- Infrastructure

# MCDA (Multi-Criteria Decision Analysis)
MCDA means, **make one decision using many criteria**. Instead of `Best = Highest economic Count`, we compute `Best =Tourists+Hotels+Economy+Accessibility+Safety+Investment` after normalizing and weighting each criterion.

- Make one decision using many criteria, use normalizing and weighting each criteria.
- common weight could be decide by: SME, Survey. But, subjectivity becomes a problem.

# Enter Entropy Weight Method (EWM)

Entropy comes from information theory.
The idea:
> More variation = more information.
> Less variation = less information.

If every destination looks almost identical for one criterion, that criterion provides little help for distinguishing them.

- comparing variance between each feature, high variance has more importance.
- This helps to decide weight for each criteria.
- Entropy comes from information theory.
  - More variation = more information.
  - Less variation = less information.
- If every destination looks almost identical for one criterion, that criterion provides little help for distinguishing them.
- High entropy
  - Everything looks similar.
  - Little useful information.
- Low entropy
  - Big differences.
  - More information.
  - More useful for ranking.
- EWM converts this into weights.

# Workflow
  - Raw Data 
  - Entropy Normalization (Column Proportion / probability normalization)
    - Shannon's Information Theory, where entropy is computed using probabilities. 
    - the entropy formula can measure how "spread out" the values are.
    - Entropy measures how much information each criterion provides.
    - Combine different criteria into one comparable score.
  - Entropy Calculation: Compute entropy -> Ej​=−k∑pij​ln(pij​), k=1/ln(m); calculate using for each row
  - Diversification degree -> dj​=1−Ej​
  - Entropy Weights: Compute weights -> wj​=​dj/∑dj​​
  - MCDA Normalization (Min-Max): Normalize for MCDA (min-max normalization)
    - This converts every criterion into the same range:
      - 0 → Worst
      - 1 → Best
    - every criterion contributes on the same numerical scale.
    - how close it is to the best-performing destination.
    - assumes every criterion has a comparable scale.
    - Each criterion now contributes proportionally according to its weight, without being distorted by differing measurement units.
    - It preserves the original ranking order.
    - Every criterion has the same range (0–1).
    - Scores are easy to interpret.
    - It works naturally with weighted-sum methods.
    - Benefit and cost criteria can be handled with simple formulas.
  - Weighted Sum Score
  - Ranking

## Advantages
  - Objective weighting: Weights are derived from the data rather than expert judgment.
  - Adaptive: Weights change automatically as new data is collected.
  - Scalable: Suitable for evaluating hundreds or thousands of destinations.
  - Transparent: The weighting process is mathematically defined and reproducible.
  - Useful for decision support: Helps identify which destinations are most competitive based on measurable indicators.

## Limitations
  - Variation is not the same as importance: An indicator may have low variation (e.g., safety) yet still be strategically important.
  - Sensitive to data quality: Missing values, outliers, or inconsistent measurements can distort entropy calculations.
  - No consideration of stakeholder priorities: EWM reflects statistical information content, not policy goals or expert preferences.
  - Requires normalization: Indicators measured in different units must be standardized before weighting.

# Dataset
### Load dataset
we use simple and common titanic dataset from seaborn library.

```python
df = pd.read_excel(r"\tours.xlsx")
```

| Destination | Tourist Arrivals | Tourism Revenue (Million $) | Hotels | Airport Accessibility |
| ----------- | ---------------- | --------------------------- | ------ | --------------------- |
| A           | 200              | 50                          | 30     | 90                    |
| B           | 500              | 80                          | 60     | 85                    |
| C           | 900              | 120                         | 120    | 70                    |
| D           | 400              | 70                          | 40     | 95                    |

## The Code
By calling, `statistic.attractiveness_ranking` we can calculate Entropy Weight Method (EWM) weights and Weighted Sum Model (WSM) sequentially with output as:
- Value for each row/entity.
- Weight for each indicator.
- Entropy value for each indicator.

```python
result, weights, entropy= statistic.attractiveness_ranking(main_data, col_list)
```

This function requires the following parameters:
- **main_data** (`dataframe`):      Data Input
- **col_list** (`List`):            list of indicator/column that we want to calculate  

## The result

- **Weight**

```python
Tourist Arrivals               0.391330
Tourism Revenue (Million $)    0.150743
Hotels                         0.438902
Airport Accessibility          0.019024
```

- **Entropy**

```python
Tourist Arrivals               0.907490
Tourism Revenue (Million $)    0.964364
Hotels                         0.896244
Airport Accessibility          0.995503
```

- **Result**

| Tourist Arrivals | Tourism Revenue (Million $) | Hotels | Airport Accessibility | Score | Rank |
| ---------------- | --------------------------- | ------ | --------------------- | ----- | ---- |
| 0.00             | 0.00                        | 0.00   | 0.8                   | 0.02  | 4    |
| 0.43             | 0.43                        | 0.33   | 0.6                   | 0.39  | 2    |
| 1.00             | 1.00                        | 1.00   | 0.0                   | 0.98  | 1    |
| 0.29             | 0.29                        | 0.11   | 1.0                   | 0.22  | 3    |


# Time Complexity
For a dataset with m destinations and n criteria:

| Step                       | Complexity |
| -------------------------- | ---------- |
| Column normalization       | O(m × n)   |
| Entropy calculation        | O(m × n)   |
| Weight calculation         | O(n)       |
| Min-Max normalization      | O(m × n)   |
| Weighted score calculation | O(m × n)   |

Overall complexity is O(m × n), making EWM + MCDA efficient enough to rank thousands of entities data.
