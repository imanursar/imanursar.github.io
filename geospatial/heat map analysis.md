---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: heat map analysis
parent: Geospatial
nav_order: 1
---

# Optimizing Cross-Docking Location Through Heat Map Analysis
<img src="/assets/images/geospatial/heat_map.png" alt="drawing" width="500"/>


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

<img src="/assets/images/geospatial/obj1.png" alt="drawing" width="300"/>
<img src="/assets/images/geospatial/obj2.png" alt="drawing" width="300"/>


## Schema
<img src="/assets/images/geospatial/schema.png" alt="drawing" width="500"/>


## Overview of the tool
<img src="/assets/images/geospatial/overview.png" alt="drawing" width="500"/>


## Dataset - Potential customer
<img src="/assets/images/geospatial/scrap.png" alt="drawing" width="500"/>
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


## Result
<img src="/assets/images/geospatial/map.gif" alt="drawing" width="500"/>

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


## Reference


## Repository

