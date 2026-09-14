---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Analytic Hierarchy Process (AHP)
parent: Scoring
permalink: /Scoring/ahp
nav_order: 103
---

# Analytic Hierarchy Process (AHP)

scoring
{: .badge .badge-pill .badge-primary }
hierarchy
{: .badge .badge-pill .badge-secondary }
ranking
{: .badge .badge-pill .badge-info }

* Do not remove this line (it will not be displayed)
{:toc}

## Introduction
  The Analytic Hierarchy Process (AHP), is a decision-making method used by individuals and organizations to rank alternatives they are considering based on pairwise comparisons (Saaty 1977, 1980).

  The Analytic Hierarchy Process (AHP) is a multi-criteria decision analysis (MCDA) method that begins by breaking down decisions into a hierarchical structure of a decision-making goal, criteria and alternatives.

  The criteria are then weighted and the alternatives scored relative to each other based on the decision-maker performing a series of pairwise comparisons. This weighting and scoring process leads to the generation of a total score for each alternative, by which they are ranked.

## AHP A five-step overview
  - **Structure the hierarchy**
    - Organize the main components of your decision-making problem into a hierarchy comprising at least three levels:
      - The over-arching decision-making goal you are trying to achieve (objective)
      - Your criteria, and, potentially, any sub-criteria, you are basing the decision on
      - The alternatives you are considering 
  - **Pairwise compare your criteria**
    - Assess the relative importance of your criteria (and, potentially, sub-criteria).
    - This is the initiate to create a series of pairwise comparisons matrix.
    - Then for criterion A versus C, and A versus D, B versus C, etc, until you have pairwise compared all your criteria.
    - Fundamental to AHP is the requirement that you answer the pairwise comparison questions by choosing your answer from a nine-point scale representing the intensity of your preferences, ranging from “equally important” (ratio = 1) to “extreme importance” (ratio = 9).
  - **Evaluate alternatives**
    - Rate the alternatives you are considering on the criteria.
    - This evaluation is performed in a similar fashion to how you assessed the relative importance of your criteria, but this time involving a series of pairwise comparisons.
    - These pairwise comparisons are performed for every pair of alternatives on every criterion.
  - **Combine weights and scores to rank alternatives**
    - combining the criterion weights from step 3 with the alternatives’ scores from step 5 by multiplying and summing them to get a total score for each alternative, by which they can be ranked.
  - **Find the Priority Index for Each Attribute or Criterion**
    - we perform a series of mathematical operations on the comparison matrix to calculate the priority index, which shows the relative importance of each criterion.
  - **Find the Consistency Ratio**
    - Discover the Consistency Ratio: A crucial measure for performing AHP effectively and achieving accurate decision-making.
    - The consistency ratio is a metric that defines whether the model based on our selection of criteria is consistent or not. 
    - We know that the model is consistent if the CR is less than 0.1.
  - **Find the Priority Index of the Suppliers Based on Each Criterion**
    - Utilize AHP to determine suppliers’ priority index by evaluating criteria and making informed decisions efficiently.

### Load dataset
  This example is often used in Saaty's expositions of the AHP as a brief but clear demonstration of the method. The data came from 30 participants were asked to compare the relative consumption of drinks in the United States. For instance, they believed that coffee was consumed much more than wine, but at the same rate as milk. The matrix derived from their answers was as follows:

  ||Coffee|Wine|Tea|Beer|Soda|Milk|Water|
  |-|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
  |Coffee|1|9|5|2|1|1|1/2|
  |Wine|1/9|1|1/3|1/9|1/9|1/9|1/9|
  |Tea|1/5|3|1|1/3|1/4|1/3|1/9|
  |Beer|1/2|9|3|1|1/2|1|1/3|
  |Soda|1|9|4|2|1|2|1/2|
  |Milk|1|9|3|1|1/2|1|1/3|
  |Water|2|9|9|3|2|3|1|

  ```python
  columns = ['Coffee', 'Wine', 'Tea', 'Beer', 'Soda','Milk', 'Water']
  data_df = pd.DataFrame(data, columns=columns)
  data_df['params'] = columns
  data_df.set_index('params',inplace=True)
  ```

## The Code
  By calling, `statistic.ahp_model` we can generate AHP model with 2 types of apporach to calculate AHP. The steps as follow:

  - It check from `is_paired` if the data has matrix paired or a single column with each value for row.
  - type 1 creates a normalized pairwise comparison matrix and dividing each column cell value with the sum of the respective column.
  - type 2 creates pairwise comparison matrix to calculate a criterion weights and alternatives’ scores. Next, we multiplying and summing them to get a total score for each alternative, by which they can be ranked.

  ```python
  priority_df, consistency_ratio = statistic.ahp_model(main_data, is_paired=True, col_list = ['params','value'], col_list_detail=[], random_input_matrix=None, detail_data:pd.DataFrame=None, types=1, epsilon=0.0001)
  ```

  This function requires the following parameters:
  - **main_data** (`dataframe`):      Data Input
  - **is_paired** (`boolean`):        Determine is the process needs to create pairwise comparison matrix or not.
  - **col_list** (`list`):            list of the columns to create pairwise comparison matrix that contains name of object and it value.
  - **col_list_detail** (`list`):     For multiple layer of AHP, this list is detail what parameters that we want to used.
  - **random_input_matrix** (`list`): List of random value to calculate consistency ratio.
  - **detail_data** (`boolean`):      Dataframe contains each criteria and rang value to create a pair-wise comarison matrix.
  - **types** (`int`):                Determine which type you want to run.
  - **epsilon** (`float`):            Acceptance error for iteration from type 2.
## Example

  ```python
  priority_df, consistency_ratio = statistic.ahp_model(data_df, types=1)
  ```

  ```python
  priority_df, consistency_ratio = statistic.ahp_model(data_df, types=2)
  ```

  This function requires the following parameters:
  - **main_data** (`dataframe`):      Data Input
  - **objectives** (`list`):          List of objective with max min value.
  - **weights** (`list`):             List of weight value between 0 - 1.
  - **alt** (`str`):                  name for each row or alternative.
  - **type** (`str`):                 Type of MDCA algorithm.
  - **is_plot** (`boolean`):          to show plot for MDCA algorithm.
  - **threshold** (`list`):           list of threshold for electra algorithm.
  - **non_dominated** (`boolean`):    filter out for non-dominated row or alternative.
  - **target_sum** (`str`):           calculate weight value with 3 type of calculation `matrix`, `weights`, `both`.

## The result
### Type 1

  | params         | Coffee  | Wine     | Tea      | Beer     | Soda     | Milk    | Water    |
  | -------------- | ------- | -------- | -------- | -------- | -------- | ------- | -------- |
  | priority index | 0.17756 | 0.019542 | 0.042139 | 0.117298 | 0.188838 | 0.12959 | 0.325032 |

  ```
  The Consistency Index is: 0.03
  The Consistency Ratio is: 0.023
  The model is consistent. it's has consistency ratio less than 0.1
  ```

### Type 2

  | params         | Coffee   | Wine     | Tea      | Beer     | Soda     | Milk     | Water    |
  | -------------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
  | priority index | 0.177457 | 0.019149 | 0.041831 | 0.116417 | 0.189572 | 0.128781 | 0.326793 |

  ```
  The Consistency Index is: 0.029
  The Consistency Ratio is: 0.022
  The model is consistent. it's has consistency ratio less than 0.1
  ```

### Other example wtih sub-criteria

  - Value of each criteria (`df`)

    | params         | Value   |
    | -------------- | ------- |
    | serviceability | 10  |
    | supply capacity | 30  |
    | quality        | 20  |
    | cost           | 20  |
    | serviceability | 20  |

  - Value of each sub-criteria (`data_detail`)

    | Criteria        | Supplier   | value |
    | --------------- | ---------- | ----- |
    | Serviceability  | Supplier 1 | 10.00 |
    | Serviceability  | Supplier 2 | 30.00 |
    | Serviceability  | Supplier 3 | 40.00 |
    | Supply Capacity | Supplier 1 | 10.00 |
    | Supply Capacity | Supplier 2 | 40.00 |
    | Supply Capacity | Supplier 3 | 60.00 |
    | Quality         | Supplier 1 | 10.00 |
    | Quality         | Supplier 2 | 5.00  |
    | Quality         | Supplier 3 | 1.25  |
    | Cost            | Supplier 1 | 10.00 |
    | Cost            | Supplier 2 | 30.00 |
    | Cost            | Supplier 3 | 2.50  |


  ```python
  priority_df, consistency_ratio, rest = statistic.ahp_model(df, is_paired=False, col_list=['params','value'],col_list_detail=['Supplier','value','Criteria'], detail_data=data_detail)
  ```

  ```
  The Consistency Index is: 0.0
  The Consistency Ratio is: 0.0
  The model is consistent. it's has consistency ratio less than 0.1
  ```

  | Criteria   | Cost     | Quality  | Serviceability | Supply Capacity | final    |
  | ---------- | -------- | -------- | -------------- | --------------- | -------- |
  | Supplier   |          |          |                |                 |          |
  | Supplier 1 | 0.058824 | 0.153846 | 0.015625       | 0.034091        | 0.262386 |
  | Supplier 2 | 0.176471 | 0.076923 | 0.046875       | 0.136364        | 0.436632 |
  | Supplier 3 | 0.014706 | 0.019231 | 0.062500       | 0.204545        | 0.300982 |

  From the above matrix, we need to choose the supplier with the maximum sum value of the ratings. As we can see from the above matrix, the sum of weights or ratings is the maximum for Supplier 2; hence it should be our choice of supplier to ensure optimal serviceability, supply capacity, quality, and cost.

  | params         | serviceability  | supply capacity     | quality      | cost     |
  | -------------- | ------- | -------- | -------- | -------- |
  | priority index | 0.125 | 0.375 | 0.25 | 0.25 |