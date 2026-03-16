---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: RFM analysis in Hospitality
parent: Segmentation and Clustering
permalink: /segment-cluster/rfm/
nav_order: 100
---

# RFM analysis (recency, frequency, monetary) in Hospitality
Segmentation
{: .badge .badge-pill .badge-primary }
RFM
{: .badge .badge-pill .badge-secondary }

## Problems
1. How to create an efficient campaign to get more attention from previous guests?
2. Can we identify our guest behaviour to create efficient flow?
3. How to identify potential returning guest?
4. How to identify the loyal guest from their activity?
5. How to identify our guest to increase customer retention and lifetime value?
6. Can we create a personalization services for our guest?

## Targeted Marketing
<img src="/assets/images/segment_cluster/rfm/rfm_01.webp" alt="drawing"/>

## Goals
1. Guest segmentation can helps us to create an efficient campaign for better target marketing.
2. Guest segmentation can assist in many of those aspects – reducing churn, offering upsells and cross-sells to segments that are more likely to respond, increasing loyalty and referrals, selling high ticket items and more.
3. Guest segmentation can minimize marketing costs and improve Rol.
4. Guest segmentation for remarketing / retargeting campaigns.
5. Guest segmentation can helps us to understand our business better.

## Two Different Techniques to solved the issues.

### Description
- **What is the output?**
  - Groups of guests that have the same characteristics based on past behaviour.
- **How could we use it?**
  - We could iterate products for segments that are build on top of descriptive output.
- **What do we need?**
historical data

### Prediction
  - **What is the output?**
    - Predict future value of each guests. The value is defined as target value.
  - **How could we use it?**
    - We could iterate products for segments that are build on top of Predicted future output.
  - **What do we need?**
    - historical data
    - Target variable

## Description —> RFM analysis

| Questions | Meaning |
| ----------------------- | ------------------------------------------ | 
| WHAT  | It is a proven marketing model for behaviour based guest segmentation | 
| HOW | It groups customers based on their transaction history – how recently (Recency), how often (Frequency) and how much did they buy (Monetary) |
| WHY | Judging guest value on just one aspect will give an inaccurate report of the guest base and their lifetime value |
| WHEN  | If there are sufficient guests and transactions and there is initiation to create efficient campaign |
| WHO  | Marketing, revenue and finance division |

## RFM analysis
We use past guest behaviour to differentiate/segment similar guests into one group.

What metrics we could use to segment guests? 
It could be driven by business processes. i.e. Recency, Frequency and Monetary, or we can use Promo, Duration, Engagement.

<img src="/assets/images/segment_cluster/rfm/rfm_02.webp" alt="drawing"/>

## Marketing Activities

<img src="/assets/images/segment_cluster/rfm/rfm_03.webp" alt="drawing"/>

## How to define the number of segment?

<img src="/assets/images/segment_cluster/rfm/rfm_04.webp" alt="drawing"/>

## How much segments that we need?
It depends on the type of business that is running

as example:

<img src="/assets/images/segment_cluster/rfm/rfm_05.webp" alt="drawing"/>

## Now, What We Have?

<img src="/assets/images/segment_cluster/rfm/rfm_06.webp" alt="drawing"/>

## What We Found?

<img src="/assets/images/segment_cluster/rfm/rfm_07.webp" alt="drawing"/>
<img src="/assets/images/segment_cluster/rfm/rfm_08.webp" alt="drawing"/>
<img src="/assets/images/segment_cluster/rfm/rfm_09.webp" alt="drawing"/>

## Quantiles selection

With Quantiles selection method we found there are 7 segments from our data. 

Quantiles = 0.2 , 0.5 , 0.8

<img src="/assets/images/segment_cluster/rfm/rfm_10.webp" alt="drawing"/>

<img src="/assets/images/segment_cluster/rfm/rfm_20.webp" alt="drawing"/>

## K-mean

from K-mean method, we found that there are around 8 - 10 segments.

evaluation score:
- elbow 	    	    ~ 9 segments
- silhouette		    ~ 8 segments
- Calinski - harabasz ~ 4 segments
- Davies Bouldin	    ~ 8 segments
- BIC			        ~ 10 segments

the main purpose of all evaluation values is to minimize intra-cluster value and maximize extra-cluster value

<img src="/assets/images/segment_cluster/rfm/rfm_11.webp" alt="drawing"/>

Result from K-mean with 8 segments.

<img src="/assets/images/segment_cluster/rfm/rfm_12.webp" alt="drawing"/>

<img src="/assets/images/segment_cluster/rfm/rfm_13.webp" alt="drawing"/>

<img src="/assets/images/segment_cluster/rfm/rfm_21.webp" alt="drawing"/>

## Interpretation

<img src="/assets/images/segment_cluster/rfm/rfm_14.webp" alt="drawing"/>

## What next? 
### the treatment
we can continue to create intervention segmentations base on guest segmentation criteria.

i.e. assign a treatment to some segments like:
1. Activation
  - Create brand awareness
  - Offer Membership / Promo / Reward
  - Make limited time offers

2. Upselling / Cross-selling
   - Upsell higher value products
   - Create brand awareness

3. Churn prevention
   - Recommend popular products
   - Renewals at discount
   - Send personalized emails to reconnect

<img src="/assets/images/segment_cluster/rfm/rfm_15.webp" alt="drawing"/>

### A/B Testing

<img src="/assets/images/segment_cluster/rfm/rfm_16.webp" alt="drawing"/>

<img src="/assets/images/segment_cluster/rfm/rfm_17.webp" alt="drawing"/>

<img src="/assets/images/segment_cluster/rfm/rfm_18.webp" alt="drawing"/>

### More variables
Objective: Combine with other guest variables to make clearer interpretation.

- Age
- Gender
- Area

i.e. with those variables we can explain more about guest behaviour and can create more clear decision treatment to some segments

### Prediction
It learns the **function** that **maps** an **input** to an **output** based on example input-output pairs.

### Action Items
Objective: Determine how much segment that we need and what treatment that we give to them  

need some advice from marketing and product team about:
- How much segment that we need 
- What treatment we will give to them
- How often we will conduct this calculation
- How to get the result (metabase?)











