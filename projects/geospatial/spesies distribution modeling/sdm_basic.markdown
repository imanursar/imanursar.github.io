---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title:  Species Distribution Modeling (SDMs) in a nutshell
parent: Species Distribution Modeling
grand_parent: Geospatial
permalink: /geospatial/sdm/sdm_basic/
nav_order: 1
---

# Species Distribution Modeling (SDMs) in a nutshell
geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
distribution models
{: .badge .badge-pill .badge-info }

* Do not remove this line (it will not be displayed)
{:toc}

# What is Species Distribution Modeling (SDM)?
At its core, **Species Distribution Modeling (SDM)** is about estimating _where a species can live_ based on environmental conditions.

## ELI5 version
Imagine we’re trying to figure out where a specific plant can grow. We notice:
- It grows where it’s cool
- It needs a lot of rain
- It prefers high elevation

Now we look at a map and highlight all places with similar conditions → that’s our predicted habitat.

That’s SDM:  

> Find the relationship between where species are found and the environment, then predict where else they could exist.

Think of SDM as:

> A spatial recommender system for nature
> It’s: Environment → species

## Formal Definition (Technical View)
SDM estimates a function:

$P(\text{species presence} \mid \text{environmental variables})$

Where:
- Inputs (features): temperature, rainfall, elevation, soil, land cover, etc.
- Output: probability (or suitability) of species presence

This is essentially a **spatial machine learning problem**.

## Data Required
There are two main data types:
1. Species data
  - Presence-only (e.g., sightings, GBIF data)
  - Presence–absence (survey data)
  - Abundance (counts)
2. Environmental predictors
  - Climate (temperature, precipitation)
  - Topography (elevation, slope)
  - Land use / land cover
  - Soil, vegetation indices (NDVI)
  - Remote sensing rasters

---

# SDM Using Machine Learning Paradigms
## Supervised Learning for SDM

### Concept
we have labeled data:
- Presence = 1
- Absence = 0

we train a model:
$f(X) \rightarrow Y$

### Common Algorithms
- Logistic Regression
- Random Forest
- Gradient Boosting (XGBoost, LightGBM)
- Neural Networks
- Support Vector Machines

### Workflow
1. Collect presence–absence data
2. Extract environmental variables at those locations
3. Train model
4. Predict across raster grid

### Example

| Location | Temp | Rainfall | Elevation | Presence |
|----------|------|----------|-----------|----------|
| A        | 20   | 2000     | 500       | 1        |
| B        | 35   | 500      | 50        | 0        |

Model learns patterns → predicts new areas.

### Strengths
- High predictive power
- Flexible
- Can model nonlinear relationships

### Weakness
- Needs absence data (often unavailable)
- Sensitive to sampling bias

---

## Unsupervised Learning for SDM
### Concept
No labels (presence/absence). We discover structure in environmental space.

### Methods
- K-means clustering
- Hierarchical clustering
- PCA + clustering
- Gaussian Mixture Models

### How it works
1. Cluster environmental conditions
2. Identify clusters where species occurs
3. Map those clusters spatially

### ELI5
Group all environments into types:
- Cool & wet
- Hot & dry

Then say:
> Species lives in cluster #3 → map all areas in cluster #3

### Limitation
- Not directly predictive
- Less precise than supervised models

---

## Maximum Entropy modeling (MaxEnt)
This is the most famous SDM method.

### Core Idea
MaxEnt estimates a probability distribution that:
- Matches known presence data
- Is otherwise as uniform (maximum entropy) as possible

### ELI5
We only know where animals were seen, not where they are absent.

So we:
1. Look at environments where they exist
2. Assume: ***They prefer these conditions***
3. Predict other places with similar conditions

Without making extra assumptions.

### Mathematical intuition
Maximize entropy:

$H(p) = -\sum p(x)\log p(x)$

Subject to constraints: Environmental averages match observed data

### Why MaxEnt is powerful
- Works with presence-only data
- Handles incomplete datasets
- Performs well with small samples

### Output
- Habitat suitability map (0–1 probability)

### Weakness
- Sensitive to sampling bias
- Assumes equilibrium (species fully occupies niche)

---

## Other SDM Methods

### BIOCLIM (Envelope Model)
- Uses min/max ranges of variables
- Simple threshold-based

ELI5:
> Species lives where temperature is between 15–25°C

Weakness:
- Oversimplified
- Ignores interactions

### Generalized Linear Models (GLM)
Classic statistical approach:

$\text{logit}(P) = \beta_0 + \beta_1 X_1 + ...$

Advantages:
- Interpretable
- Good baseline

### Generalized Additive Models (GAM)
Advantages:
- Nonlinear smooth functions
- More flexible than GLM

### Random Forest / Ensemble Models
Advantages:
- Combine multiple models
- Often best performance

### Deep Learning (CNN, spatial models)
Advantages:
- Uses raster stacks as input
- Captures spatial patterns

### Mechanistic Models (Process-based)
Instead of learning from data:
- Use biological rules
- e.g., temperature tolerance, metabolism

### Joint Species Distribution Models (JSDM)
Advantages:
- Model multiple species together
- Captures interactions (competition, symbiosis)

## Key Assumptions in SDM
1. Species–environment equilibrium: Species occupies all suitable habitats
2. Stationarity: Relationships don’t change over space/time
3. No sampling bias: Data represents true distribution
4. Environmental variables are sufficient: Missing variables = wrong predictions

This is critical to validate the key assumptions in SDM.

## Limitations & Constraints
1. Sampling Bias: Data often comes from easy-to-access areas. This would lead to biased models if not handle with caution.
2. Absence Data Problem: True absence is hard to confirm. This would generate pseudo-absence that introduces noise.
3. Spatial Autocorrelation: Nearby locations are similar → violates independence.
4. Climate Change / Non-stationarity: Models trained on past data may fail in future conditions
5. Ignoring Biotic Interactions:
  - Predators
  - Competition
  - Human activity
6. Scale Sensitivity: Resolution of raster affects results
7. Overfitting: Complex models (RF, DL) may memorize noise
8. Extrapolation Risk: Predicting outside training conditions is unreliable.

## Is SDM Species-Specific?
Short answer: No — it’s a general modeling framework.

It’s just:

> Predict spatial distribution of something based on features

## Other Applications (Beyond Species)
SDM concepts are widely reused:
1. Disease Mapping
  -  Malaria risk
  - Dengue spread

Predict: $P(\text{disease occurrence} \mid environment)$

2. Urban & Human Geography
  - Population distribution
  - Crime hotspots
3. Agriculture
  - Crop suitability
  - Yield prediction zones
4. Business / Location Intelligence
  - Store placement
  - Customer density
5. Environmental Risk
  - Landslides
  - Flood risk
  - Wildfire susceptibility
6. Invasive Species Prediction
  - Where species might spread
7. Conservation Planning
  - Identify biodiversity hotspots
  - Habitat protection prioritization

# SDM vs Interpolation (IDW, Kriging, Nearest ND)

Both models that *look similar on the surface (both produce spatial maps)* but are fundamentally different in **what they model and what assumptions they make**.

## Core Difference (High-Level)
- SDM (Species Distribution Modeling): Learns relationship between environment and occurrence
- Interpolation (IDW, Kriging, Nearest ND): Estimates values between known points based on spatial proximity

## ELI5
- SDM: This animal likes cold + wet → find all places like that.
- Interpolation: I measured temperature at 10 points → guess temperature in between.

## Mathematical Perspective
### SDM (Predictive / Causal-ish Model)
we model:

$P(\text{presence}) = f(\text{temperature, rainfall, elevation, ...})$

- Feature-driven
- Not purely spatial
- Can predict outside sampled locations

### Interpolation (Spatial Estimation)
we model:

$Z(x) = \sum w_i Z(x_i)$

- Only depends on neighboring points
- No environmental understanding
- Assumes spatial continuity

- Inverse Distance Weighting (IDW)
	- Nearby points matter more:
	
	- $Z(x) = \frac{\sum \frac{Z_i}{d_i^p}}{\sum \frac{1}{d_i^p}}$
	
	- ELI5: Closer points are more similar than far ones
	- Characteristics
    - Deterministic
    - No statistical model
    - Smooth surface
    - No uncertainty estimate
	- When it works
    - Dense, evenly spaced data
    - Smooth phenomena (temperature, elevation)
  - Problem
    - Cannot capture complex patterns
    - Sensitive to clustering

- Kriging (Geostatistical Model)
	- Uses spatial autocorrelation structure
  - Key idea:

	- $\text{Covariance depends on distance}$

	- ELI5: Not just distance, but how similarity changes with distance.
	- Components:
    - Variogram (core of Kriging)
    - Spatial dependence modeling
	- Advantages
  	- Statistically optimal (under assumptions)
  	- Provides uncertainty (variance)
  	- Handles spatial structure better than IDW
	- Weakness
  	- Requires strong assumptions (stationarity)
  	- Complex to tune
  	- Computationally expensive

- Nearest ND Interpolator (Nearest Neighbor)
	- Assign value of closest point:

	- $Z(x) = Z(x_{\text{nearest}})$

	- ELI5: Just copy the closest value
	- Characteristics
  	- No smoothing
  	- Produces blocky / discrete map
  	- Very fast
	- Use case
  	- Categorical data (land cover, class labels)

## SDM vs Interpolation

| Aspect | SDM | IDW / Kriging / Nearest |
|------|-----|--------------------------|
| Goal | Predict **suitability / probability** | Estimate **continuous value** |
| Input | Environment + occurrences | Observed values at points |
| Output | Probability / suitability map | Continuous surface |
| Learning | Yes (ML/statistical) | No (except Kriging partially) |
| Extrapolation | Yes (to new environments) | No (only spatial interpolation) |
| Drivers | Environmental variables | Distance / spatial structure |
| Use case | Ecology, habitat modeling | Temperature, rainfall, elevation |

## Critical Concept: Spatial vs Environmental Space

### Interpolation = Geographic Space
- Depends on: Distance in coordinates (x, y)
- IDW/Kriging: different

### SDM = Environmental Space
- Depends on: Distance in feature space
- Two locations:
  - Far geographically
  - But identical climate
- SDM: similar

## Why Interpolation ≠ SDM
- Interpolation assumes: Nearby locations are similar
- Species distribution depends on:
  - Climate
  - Habitat
  - Ecology
	- NOT just distance.




























