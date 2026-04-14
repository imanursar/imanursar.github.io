---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Transformations Parameters
parent: kv - Solutions
grand_parent: Knowledge Vaults
permalink: /knowledge-vaults/solutions/transform
nav_order: 14
---

# Transformations Parameters
Solutions
{: .badge .badge-pill .badge-primary }

* Do not remove this line (it will not be displayed)
{:toc}


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