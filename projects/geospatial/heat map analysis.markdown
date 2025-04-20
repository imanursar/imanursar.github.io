---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Heat Map Analysis
parent: Geospatial
permalink: /geospatial/heat map analysis/
nav_order: 2
---

# Optimizing Cross-Docking Location Through Heat Map Analysis

geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
heatmap
{: .badge .badge-pill .badge-info }

<img src="/assets/images/geospatial/cross_dock.webp" alt="drawing" width="500"/>

## Introduction
<p style='text-align: justify;'>
In the rapidly evolving landscape of logistics, the efficiency of last-mile delivery has become a critical factor in maintaining competitive advantage and customer satisfaction. By using direct shipping from distribution centers to individual buyers, leading to increased costs and extended delivery times, particularly in densely populated or geographically dispersed areas.</p>

<p style='text-align: justify;'>
To address these challenges, our team has developed a data-driven tool designed to analyze and visualize the distribution of buyers, potential buyers, and transaction data across specific regions.</p>

<p style='text-align: justify;'>
By leveraging this tool, we can generate heat maps that pinpoint high-density areas of demand and transaction volume, offering valuable insights into where logistical improvements can be made. By utilizing heat maps, we can more accurately identify optimal Cross-Docking that align with buyer and transaction concentrations. These identified zones can then be pursued as cross-docking locations to optimize last-mile logistics.</p>


## Objective
<p style='text-align: justify;'>
The primary objective of this doc is to demonstrate how our tool's heat map analysis can inform and optimize cross-docking decisions. By identifying the most strategic Cross-Docking, we aim to significantly reduce last-mile delivery costs while maintaining or even improving service levels.</p>

<img src="/assets/images/geospatial/heat_map/obj_1.webp" alt="drawing" width="300"/>
<img src="/assets/images/geospatial/heat_map/obj_2.webp" alt="drawing" width="300"/>


## Schema
<img src="/assets/images/geospatial/heat_map/schema.webp" alt="drawing" width="500"/>


## Overview of the tool
<img src="/assets/images/geospatial/heat_map/overview_tool.webp" alt="drawing" width="500"/>


## Dataset - Potential customer
<img src="/assets/images/geospatial/heat_map/scrap.webp" alt="drawing" width="500"/>
<p style='text-align: justify;'>
We aggregate potential data from Google Maps by targeting specific customers, locations, and keywords.

By identifying the business type through Google Maps, we classify them into three channel types:</p>
<ul>
    <li>General Trade</li> 
    <li>Modern Trade</li>
    <li>Horeca</li>
</ul>

Once all data is collected, we estimate metrics such as tonnage, sales orders, and GMV using historical data specific to each city and channel type. 

The median monthly values are then determined as the estimation benchmarks for each parameter. We also use this estimation benchmarks for buyer leads data.


## Heat-Map Result
<img src="/assets/images/geospatial/heat_map/map.gif" alt="drawing" width="500"/>

<p style='text-align: justify;'>
By comparing these three heatmaps (Potential data, Registered data, Transaction data), we can identify the most strategic Cross-Docking based on three key parameters:
<ul>
    <li>Areas with future growth potential and opportunities for generating additional demand.</li> 
    <li>Geographic locations where sales demand is concentrated.</li>
    <li>Regions with a high level of current business activity.</li>
</ul>

This analysis enables us to determine optimal Cross-Docking locations based on data insights, helping us to identify high-density areas that could reduce last-mile delivery costs if selected as cross-docking points.</p>

<p style='text-align: justify;'>
Additionally, these maps can serve several other purposes, such as:
<ul>
    <li>Differentiating areas with frequent low-volume transactions from those with fewer high-volume transactions to inform logistical planning.</li>
    <li>Determining which areas to prioritize if we aim to maintain current transaction levels, potentially reducing delivery distances and times.</li>
    <li>Spotting regions with high transaction volumes occurring away from dense buyer areas for potential strategic initiatives.</li>
    <li>Identifying areas where we have a higher concentration of buyer leads compared to others, and understanding the reasons behind it.</li>
    <li>Recognizing patterns in the distribution of our buyer leads.</li>
    <li>Combining this data with customer segmentation and behavior (e.g., new, retention, churn) to pinpoint areas where we should focus our outreach efforts.</li>
    <li>Detecting high-potential buyer densities or high-transaction buyer densities that may not align with current buyer distributions.</li>
    <li>Identifying regions suitable for expansion or targeted marketing campaigns.</li>
</ul>
And many more insights
</p>


## Heat-Map with Analysis of matrices
<img src="/assets/images/geospatial/heat_map/map_adv.gif" alt="drawing" width="500"/>

<p style='text-align: justify;'>
In addition to the heatmap visualizations provided by this tool, we can perform a deep dive analysis of tonnage, GMV, and sales orders within the identified regions.

By leveraging these visualizations and analytics, we can discuss and assess the logistical implications.

In example: particularly in high-volume areas within a 5 km radius of selected points of interest:
<ul>
    <li>The number of potential buyers, buyer leads, and transactions</li>
    <li>The distribution across different channel categories</li>
    <li>Identifying the direction of the highest concentration of buyers near this point.</li>
    <li>Analyzing and comparing key metrics within the radius area, including: Tonnage, GMV, Sales orders</li>
</ul>

Further breakdowns could include:
<ul>
    <li>Detailed analysis of the above metrics by channel category (GT, MT, HoReCa) and/or by kabupaten or city within the radius.</li>
    <li>Using historical data to estimate the potential market size within the radius.</li>
</ul>
</p>
<br>

<img src="/assets/images/geospatial/heat_map/table_1.webp" alt="drawing" width="500"/>
<p style='text-align: justify;'>
As shown in the table above, we can measure the number of potential and registered buyers, the required tonnage, GMV, and sales orders generated for each city and channel category. This insight is crucial for formulating a strategic plan for the area, from both business and logistics perspectives.
</p>


## Comparing two points to get more insight and decision
<p style='text-align: justify;'>
With this tool, we can comparing 2 points that lead us to get more insight and better decision for cross-docking location.
</p>

#### East Jakarta

<img src="/assets/images/geospatial/heat_map/map_adv_2.gif" alt="drawing" width="500"/>
<p></p>
<img src="/assets/images/geospatial/heat_map/table_2.webp" alt="drawing" width="425"/>
<img src="/assets/images/geospatial/heat_map/table_3.webp" alt="drawing" width="425"/>

#### South Jakarta

<img src="/assets/images/geospatial/heat_map/map_adv_3.gif" alt="drawing" width="500"/>


## Expansion
<p style='text-align: justify;'>
if we want to expand our business by establishing a new Cross-Docking in a high-potential area like Bogor. First, we need to identify regions with a high density of potential buyers, registered buyers, and areas with high order volumes. With this information, we can select the most optimal location for a Cross-Docking that would efficiently cover both existing transactions and potential buyers.
</p>

#### Bogor
<img src="/assets/images/geospatial/heat_map/map_adv_4.gif" alt="drawing" width="500"/>

#### West Jakarta
<img src="/assets/images/geospatial/heat_map/map_adv_5.gif" alt="drawing" width="500"/>

#### Surabaya
<img src="/assets/images/geospatial/heat_map/map_adv_6.gif" alt="drawing" width="500"/>

#### Bali
<img src="/assets/images/geospatial/heat_map/map_adv_7.gif" alt="drawing" width="500"/>

#### Bekasi
<img src="/assets/images/geospatial/heat_map/map_adv_8.gif" alt="drawing" width="500"/>


## Key Takeaways 
<ul>
    <li>This tool and its visualizations allow us to gain deeper insights into the distribution of buyers, potential buyers, and transaction data across specific regions.</li>
    <li>Comparing three parameters—potential buyers, registered buyers, and transaction buyers—helps us identify areas with high and low buyer activity.</li>
    <li>Enables a better understanding of the potential market, retention opportunities, and areas with high transaction volume.</li>
    <li>Facilitates the calculation of key metrics for single or multiple points, providing a comprehensive view to determine optimal locations for Cross-Dockings or distribution centers.</li>
    <li>offering valuable insights into where business and logistical improvements can be made.</li>
    <li>Supports the initiation of cost-distance and cost-benefit analyses.</li>
</ul>


