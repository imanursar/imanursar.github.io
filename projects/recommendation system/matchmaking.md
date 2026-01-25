---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Matchmaking
parent: Recommendation System
permalink: /recommendation system/matchmaking
nav_order: 102
---

# Optimizing Supply and Demand Matchmaking

Recommendation
{: .badge .badge-pill .badge-primary }
Optimization
{: .badge .badge-pill .badge-secondary }
matchmaking
{: .badge .badge-pill .badge-info }

<img src="/assets/images/recommendation/supply_demand.png" alt="drawing" width="500"/>

* Do not remove this line (it will not be displayed)
{:toc}

## Introduction
<p style='text-align: justify;'>
The efficient alignment of supply and demand is a critical challenge for each transaction operation.</p>

<p style='text-align: justify;'>
The biggest challenge is to identify the most suitable suppliers to fulfill the varying demands listed by our bussiness team. This process often results in suboptimal supplier choices, delayed order fulfillment, and increased costs, ultimately impacting customer satisfaction and overall business performance.</p>

<p style='text-align: justify;'>
Given these challenges, there is a critical need for a more structured approach to supply-demand matching that leverages data-driven insights and predictive modeling. By refining the supplier selection process, we can improve order generation rates, enhance fulfillment accuracy, and reduce the time to market.</p>

<p style='text-align: justify;'>
To address these challenges, we have developed a tool that streamlines the matchmaking process between supply and demand for each transaction operation.</p>


## Objective
<p style='text-align: justify;'>
The primary objective of this project is to enable the business team to efficiently find the best suppliers for the listed demand, enhancing order generation and improving the fulfillment process.</p>

<p style='text-align: justify;'>
By integrating data from both internal systems and the harvest prediction model, the tool provides reliable, almost real-time supplier recommendations, ensuring high-quality supply sources that meet our business requirements.</p>

<img src="/assets/images/recommendation/matchmaking/issue.png" alt="drawing" width="175" height='300'/>


## Schema
<img src="/assets/images/recommendation/matchmaking/schema.png" alt="drawing" width="500"/>


## Overview of the tool
<img src="/assets/images/recommendation/matchmaking/overview_tool.png" alt="drawing" width="500"/>


## Key Parameters for Matchmaking
<p style='text-align: justify;'>
The core functionality of this tool is a scoring process designed to identify the best-matching supplies for the given demand.</p>

This process is divided into four steps:
- **Mandatory Parameters**: assess the most critical factors
- **Main Parameters**: evaluate additional important factors
- **Scoring Parameters**: Combines multiple criteria to recommend only the most suitable suppliers.
- **Ranking**: sorting all result to give the best supplier


## Scoring and Recommendation Process
<p style='text-align: justify;'>
Once the user inputs the data, the tool matches the demand with the existing entries from the supplies datasets. The output consists of two tables, one for each data source, along with additional details about the scoring process.
</p> 

Key columns include:
- **Rank**: Indicates the best supplier.
- **Final_Score**: Represents the overall matchmaking score.
- **Source_Rec**: Recommends the most profitable delivery type.
- **Distance_Rec and Distance_in_km**: Show the distance detail between supply and demand.
- **Tonnage_Ratio_Supply_Demand**: Indicates the percentage of supply tonnage that matches the demand.
- **Margin**: Calculates the potential margin generated from matching the supply with the demand.


## Result
<img src="/assets/images/recommendation/matchmaking/result_1.png" alt="drawing" width="500"/>
<img src="/assets/images/recommendation/matchmaking/result_2.png" alt="drawing" width="500"/>


## The Key Benefits
Implementing this tool offers several key benefits to business teams:
- **Improved Supplier Alignment and Enhanced Order Generation**: The tool enables the channel team to precisely and efficiently matching supply and demand, the tool drives increased order generation.
- **Data-Driven Decision Making**: The tool provides a transparent, objective basis for supplier selection, leveraging data from internal systems and the harvest prediction model.
- **Margin Optimization**: By choosing suppliers based on a comprehensive scoring system that includes pricing considerations (and soon will include the log cost), the tool helps reduce procurement costs.
- **Increased Fulfillment Rates and Reduced Lead Times**: With the tool's data-driven approach, we can significantly improve our fulfillment rates by selecting suppliers who can meet demand requirements promptly.
- **Upstream-downstream Connectivity**: By utilizing harvest prediction data and Kabayan data, we can prioritize farmers with AR and due dates approaching soon to become suppliers for DFF GT. This approach helps maintain the AR/AP cash flow process within Kabayan and reduces the number of farmers falling into the NPL category due to delays in AR payments.
- **Scalability and Flexibility**: The tool and its underlying model can be easily implemented across other business channels (such as Horeca and Modern Trade) or scaled to provide matchmaking recommendations at the business level.

