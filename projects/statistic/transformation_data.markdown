---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Transformations Parameters
parent: Statistics
permalink: /statistics/transform
nav_order: 103
---

# Transformations Parameters
Solutions
{: .badge .badge-pill .badge-primary }

* Do not remove this line (it will not be displayed)
{:toc}

# Transformation Type

| Transformation               | Use Case                                                                                                       | Equation / Calculation Method                                                   |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Log Transformation           | Stabilizing variance, normalizing data, useful for data with exponential changes (e.g., economic data).        | y = log(x)                                                                      |
| Square Root Transformation   | Stabilizing variance, normalizing data, suitable for data sets with non-negative values (counts, areas).       | y = √x                                                                          |
| Box-Cox Transformation       | Generalized form for stabilizing variance, making data more normal-like, applicable in various scenarios.      | y(λ) = (x^λ -1)/λ, for x > 0 and λ ≠ 0                                          |
| Z-Score/Standard Score       | Standardizing data to have mean of 0 and standard deviation of 1, used in outlier detection and normalization. | z = (x-µ)/σ                                                                     |
| Min-Max Scaling              | Scaling data to a fixed range (0-1), useful in scale-sensitive algorithms (neural networks, k-NN).             | Xscaled = (X - Xmin) / (Xmax - Xmin)                                            |
| Normalization (L1, L2 norms) | Scaling individual samples, essential for algorithms needing comparable scales (support vector machines).      |                                                                                 |
| Difference Transformation    | Making time-series data stationary by subtracting previous observation from the current one.                   | Δxt = xt - xt-1                                                                 |
| Categorical Encoding         | Converting categorical data into a numeric format for use in mathematical models (One-Hot, Label Encoding).    | One-Hot: Binary vectors, Label: Integer encoding                                |
| Binning/Discretization       | Transforming continuous variables into discrete bins, simplifying complex relationships in data.               | Interval: Equal-Width Quantile: Equal Frequency Count Tree-Based: Decision Tree |


# Encoding Type

| Type                         | Data Type    |  Details           | 
| ---------------------------- | ------------ | ------------------ | 
| Label Encoding     | Ordinal data | Unique labels with Equal interval     | 
| Ordinal Encoding     | Ordinal data | Same as label encoding with ordered data     |	
| Target-guided Encoding       | Ordinal data | Equal interval     |
| Polynomial Encoding          | Ordinal data | Non-Equal interval | 
| Helmert Encoding             | Ordinal data | Non-Equal interval |
| Sum/ Count Encoding          | Ordinal data | Contains count or sum for each category, Non-Equal interval |
| Backward Different Encoding  | Ordinal data | Non-Equal interval |
| One-hot Encoding             | Nominal data | Convert all categories into each column with 0 1, < 15 Cardinality, not suitable for decision-tree based algorithm |
| Dummy Encoding               | Nominal data | Same as One-hot encoding with drop one feature (randomly) |
| Effect Encoding              | Nominal data | Same as Dummy encoding with alter row with zeros to all -1 |
| Mean Encoding                | Nominal data |                    |
| Binary Encoding              | Ordinal / Nominal data | converts data into more several columns in binary labels, each colums contain 0 and 1 to label each category in binary, Some info loss acceptable for lower dimesionality |
| BaseN Encoding               | Ordinal / Nominal data |          |
| Feature Hashing Encoding     | Ordinal / Nominal data | Some info loss acceptable for lower dimesionality |
| Frequency Encoding           | Ordinal / Nominal data |          |
| LeaveOneOut Encoding         | Ordinal / Nominal data | info loss is not acceptable, the encoder can handle overfitting / response leakage |
| Target Encoding              | Ordinal / Nominal data | info loss is not acceptable, the encoder can't handle overfitting / response leakage |
| Weights of Evidence Encoding | Ordinal / Nominal data | info loss is not acceptable, the encoder can't handle overfitting / response leakage |
| James-Stein Encoding         | Ordinal / Nominal data | info loss is not acceptable, the encoder can't handle overfitting / response leakage |
| M-Estimator Encoding         | Ordinal / Nominal data | info loss is not acceptable, the encoder can't handle overfitting / response leakage |
| Generalzied Linear Mixed Model Encoding           | Ordinal / Nominal data |          |
| CatBoost Encoding            | Ordinal / Nominal data |          |
| RareLabel Encoding           | Ordinal / Nominal data |          |


# Handling Missing Data

| Type                         | Type         | Type                                             | Details          |
| ---------------------------- | ------------ | ------------------------------------------------ | ---------------- |
| Common data                  | Deletion     | Deletion                                         | Row-wise Deletion |
| Common data                  | Deletion     | Deletion                                         | Columns-wise Deletion |
| Time-Series data             | Imputation   | Mean, Median, Mode, Random Sample Imputation     | Data without Trend and without seasonality |
| Time-Series data             | Imputation   | Linear Interpolation                             | Data with Trend and without seasonality |
| Time-Series data             | Imputation   | Seasonal adjustment + interpolation              | Data with Trend and with seasonality |
| Common data                  | Imputation   | Make NA as level                                 | Categorical |
| Common data                  | Imputation   | Logistic Regression                              | Categorical |
| Common data                  | Imputation   | Mean, Median, Mode, Linear Regression            | Numerical   |