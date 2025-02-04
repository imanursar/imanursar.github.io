---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Credit Scoring 101
parent: Scoring
permalink: /Scoring/credit scoring 101/
nav_order: 1
---

# Credit scoring 101

scoring
{: .badge .badge-pill .badge-primary }
credit score
{: .badge .badge-pill .badge-secondary }
machine learning
{: .badge .badge-pill .badge-info }

<img src="/assets/images/scoring/credit_score_cover.png" alt="drawing" width="500"/>

## What is credit score? And why it useful
<p style='text-align: justify;'>A credit score is a numerical expression based on a statistical analysis of a person’s credit files, to represent the creditworthiness of an individual. The higher the credit score the more confident a lender can be of the applicant's creditworthiness.</p>

<img src="/assets/images/scoring/credit score/credit_score_01.png" alt="drawing" width="300"/>

## Uses of credit score
Lender, such as banks and credit card companies, use credit score to:
- evaluate the potential risk posed by lending money to consumers and to mitigate losses due to bad debt.
- Determine who qualifies for a loan, at what interest rate, and what credit limits.
- Determine which applicants are likely to bring in the most revenue.
- Automatic and fast to assess risk.


## 3 Factors that make up a credit scoring
- Five Cs Of Credit Analysis
- Historical loan
- External data


## Credit score for each stage
<img src="/assets/images/scoring/credit score/credit_score_02.png" alt="drawing" width="500"/>

- The Applicant Scoring Model (A-Score)
- The Transaction / performance Scoring Model (B-Score)
- The Collection Scoring Model (C-Score)


## How we do it? Of Course using CRISP-DM
<img src="/assets/images/scoring/credit score/credit_score_03.png" alt="drawing" width="500"/>
<img src="/assets/images/scoring/credit score/credit_score_04.png" alt="drawing" width="500"/>


## What are we targeting during prediction?
Experience in data is a historical data, and the best variable among them is the target variable. It is **the variable that we want to use the model to explain or predict** using the rest of the variables.

The target variable is usually:
- It can be 0 for performing applicants and 1 to indicate defaulted applicants.
- We can use the term defaulted applicant, when a applicant is late on their first payment (First Payment Default (FPD)).
- We can use the term defaulted applicant, when a applicant is more than 30/60/90 days late on their active tenor (Days Past Due (DPD))

In binary form, sometimes we will refer to bad applicants as the ones in some sort of default and good applicants as the others.

## 3 types of Model
- Modelling with simplest approach - rule based
- Modelling with simple approach - Scorecard
- Modelling with Machine learning approach

<img src="/assets/images/scoring/credit score/credit_score_05.png" alt="drawing" width="750"/>


## Machine learning as a black box
Machine learning has great potential for improving products, processes and research. But computers usually do not explain their predictions which is a barrier to the adoption of machine learning. 

We can use local and/or global method to interpret behavior of a machine learning model.

<img src="/assets/images/scoring/credit score/credit_score_06.png" alt="drawing" width="300"/>

## What we expect as the output here?
By using those models, we expect to get:
- Overall score value
- Probability to pay / to default
- Scorecard points

Especially form ML model, we need Interpretable model such as:
- Feature importance 
- Feature contribution

<img src="/assets/images/scoring/credit score/credit_score_07.png" alt="drawing" width="500"/>

## Developing credit score 
<img src="/assets/images/scoring/credit score/credit_score_08.png" alt="drawing" width="500"/>
<img src="/assets/images/scoring/credit score/credit_score_09.png" alt="drawing" width="500"/>
<img src="/assets/images/scoring/credit score/credit_score_10.png" alt="drawing" width="500"/>