---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: A/B Testing Technical 101
parent: kv - Solutions
grand_parent: Knowledge Vaults
permalink: /knowledge-vaults/solutions/abtest-tech
nav_order: 103
---

# A/B Testing Technical 101 - Statistic method
Solutions
{: .badge .badge-pill .badge-primary }

* Do not remove this line (it will not be displayed)
{:toc}

## Shapiro-Wilks Test for both group
## Levene’s Test for Homogeneity of variances
## t-test for comparing groups.
## Minimum Detectable Effect (MDE) - minimum uplift yang ingin terukur

--- 

## Chi-Square Test
  - The chi-squared test (for independence) is a statistical test to evaluate whether or not the distributions of two or more categorical variables — each variable has two or more possible values— are actually independence or homogenous (i.e. how the values are distributed on the two variables are relatively the same).
  - Dataset “R×C table,” where R is the number of rows and C is the number of columns.

### Experiments with Binary Outcomes: The Chi-Squared Test
  - a binary outcome experiment has only two outcomes: either an action is taken or it isn’t.
  - we calculate the proportion of each variant that completes the action. The numerator is the number of completers, while the denominator is all units that were exposed.
  - This metric is also described as a rate: completion rate, clickthrough rate, graduation rate, and so on.
  - To determine whether the rates in the variants are statistically different, we can use the chi-squared test, which is a statistical test for categorical variables.

### Example
  - <img src="/assets/images/knowledge/solution/abtesting/abtt_01.webp" alt="drawing"/>
  - <img src="/assets/images/knowledge/solution/abtesting/abtt_02.webp" alt="drawing"/>
  - They roll the experiment by serving each of users with one of the two designs randomly and record his/her action accordingly — whether or not he/she redeems the voucher.
  - The redemption rate from the revamped design is higher than what the existing design yielded. Nevertheless, it might be the case that the difference was actually caused by some inherent random noise (not statistically significant). Using the chi-square test, it is then our task to check whether or not the difference is significant.
  - The chi-squared test is only valid if the sample size is *relatively large*, i.e. > 1000 (McDonald, 2014).
  - If this threshold is not met, the test result might be not reliable. In such cases, one can use Fisher’s exact test instead.







