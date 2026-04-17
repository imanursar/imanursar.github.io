---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Regression Analysis
parent: kv - Solutions
grand_parent: Knowledge Vaults
permalink: /knowledge-vaults/solutions/regression
nav_order: 199
---

# Regression Analysis
Regression
{: .badge .badge-pill .badge-primary }

* Do not remove this line (it will not be displayed)
{:toc}

## Defininiton
  Regression Analysis captures the relationship between one or more response variables (dependent/predicted variable – denoted by Y) and the its predictor variables (independent/explanatory variables – denoted by X) using historical observations of both.

  Its estimates the functional relationship between a set of independent variables X1, X2, …, Xp with the response variable Y which estimate of the functional form best fits the historical data.


## Type of Linear Regression

  | Dependent Variable Type | Residual Distribution           | Types of Regression        |  Details      |
  | ----------------------- | ------------------------------- | -------------------------- | ------------- |  
  | Continuous              | Normal (with constant variance) | Ordinary Least Squares     |               | 
  | Continuous              | Normal (without constant variance) | Generalized Least Squares     |                | 
  | Binary                  | Binomial                        | Logistic Regression     |                | 
  | Discrete                | Poisson                         | Poisson Regression     |                | 
  | Rational                | Exponential Family of Distribution | Generalized Least Squares|                | 
  |                         |                                 | Simultaneous Equation Models| When both X and Y are dependent on each other | 
  |                         |                                 | Structural Equation Models  | Captures the inter-relations between Xs (how Xs affect each other before affecting Y) | 
  |                         |                                 | Survival Analysis           | Predicts a decay curve for a probability of an event | 
  |                         |                                 | Hierarchal Bayesian         | Estimates a non-linear equation | 


## Linear Regression as Model
  - It can be used for the following two distinct but related purposes
    - Predict certain events
    - Identify the drivers of certain events based on some explanatory variables
  - Isolates individual effects and then quantifies the magnitude of that driver to its impact on the dependent variable


## Ordinary Least Squares model assumptions
- **Linearity** - Model is linear in parameters
  - Yi=a+b1X1i+b2X2i+…+bpXpi+ei
- **Spherical Errors** - Error distribution is Normal with mean 0 & constant variance
  - e2i ~ Normal(0, σ)
- **Zero Expected Error** - The expected value (or mean) of the errors is always zero
  - E(ei)=0 for all i
- **Homoskedasticity** - The errors have constant variance
  - Variance(ei)=constant for all i
- **Non-Autocorrelation** - The errors are statistically independent from one another. This implies the data is a random sample of the population
  - corr(ei, ej)=0 for all i≠j
- **Non-Multicollinearity** - The independent variables are not collinear
  - Covariance (Xi,Xj) = 0








