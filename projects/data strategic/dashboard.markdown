---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Dashboard Strategic
parent: Data Strategic
permalink: /data strategic/dashboard
nav_order: 99
---

#  Dashboard Strategic

dashboard
{: .badge .badge-pill .badge-primary }
data strategic
{: .badge .badge-pill .badge-secondary }

## What is the purpose of Dashboard?
In a nutshell, dashboards serve to understand WHAT's happening and test the common hypotheses. Thus you are very unlikely to find in available dashboards something unexpected that shifts the way you understand things.


## Dashboards are everywhere... but where are INSIGHTS?

- An INSIGHT goes way beyond just founding something "interesting" in the data.
- A metric spike can generate curiosity, but it's not an insight.
- An insight is an UNEXPECTED SHIFT in the way we understand things that inspires us to act.

## How to find real insights?

- Conduct comprehensive analysis leveraging all the available data.
- Raise an UNEXPECTED hypothesis based on data
- Bring a NEW PERSPECTIVE
- Be ACTIONABLE and aligned with key stakeholders' PRIORITIES

## Dashboards can be grouped into 3 types:

1. **STRATEGIC** dashboards are mainly used by executives to monitor KPIs. It's useful to monitor how key metrics are evolving, but no real insights.
    - Purpose: **Provide insights** into long-term strategic goals and performance.
    - Content: **Key strategic metrics**, trends, and progress toward organizational objectives.
    - Users: **Senior executives**, strategic planners, and decision-makers.
    - When: yearly, quarterly and monthly
2. **ANALYTICAL and TACTICAL** dashboards enable users to investigate trends. They can provide useful information and help users to validate or reject their hypothesis around WHY something is happening.
    - Purpose: Facilitate **in-depth data analysis** and exploration.
    - Content: **Interactive charts**, graphs, and tables for detailed data investigation and discovery.
    - Users: **Data analysts**, business analysts, and other professionals conducting in-depth analysis
    - When: quarterly, monthly and weekly
3. **OPERATIONAL** dashboards answer the question "what's happening now?". Useful to track metrics in real-time, but they don't provide real insights.
    - Purpose: **Monitor** and manage day-to-day operations and activities.
    - Content: **Real-time** or near-real-time data on key performance indicators (KPIs) and operational metrics.
    - Users: **Operations managers**, team leads, and frontline staff
    - When: weekly and daily
    - But dashboards are often not enough for operational decision-making. It's not anymore about the high-level overview. It's about optimizing daily basis.
    - Operational use cases have 3 special requirements:
        - GRANULAR data (e.g., at the campaign level), often including multiple metrics
        - SPEED to make better decisions daily (it can't wait until tomorrow or next week)
        - FLEXIBILITY to enable granular deep dives, data exploration and hypothesis testing

## For additional we can create these dashboards such as:

1. **TACTICAL** Dashboards
    - Purpose: Support **mid-term planning** and **decision-making**.
    - Content: **Tactical-level KPIs** and metrics for performance tracking and improvement.
    - Users: **Middle management**, department heads, and project managers.
2. **FINANCIAL** Dashboards
    - Purpose: **Monitor financial health** and performance.
    - Content: **Financial metrics**, budget vs. actuals, revenue, expenses, and financial forecasts.
    - Users: **CFO**, finance managers, and financial analysts.
3. **HR** dashboards
    - Purpose: **Track and manage human resources** metrics.
    - Content: **Employee performance**, recruitment metrics, turnover rates, and workforce demographics.
    - Users: **HR managers**, recruiters, and executives
4. **MARKETING** dashboards
    - Purpose: **Evaluate the effectiveness of marketing campaigns** and strategies.
    - Content: **Marketing metrics**, conversion rates, customer acquisition costs, and campaign performance.
    - Users: **Marketing managers**, analysts, and executives
5. **Customer Service** Dashboards
    - Purpose: **Monitor and improve customer service performance**.
    - Content: **Customer satisfaction scores**, response times, ticket resolution rates, and service quality metrics.
    - Users: **Customer service managers**, support teams, and executives.
6. **Supply Chain** Dashboards
    - Purpose: **Optimize and manage the supply chain process**.
    - Content: **Inventory levels**, order fulfillment metrics, supplier performance, and logistics data.
    - Users: **Supply chain managers**, logistics professionals, and operations teams
7. **Sales** Dashboards
    - Purpose: **Track and analyze sales performance**.
    - Content: **Sales metrics**, revenue, conversion rates, and pipeline analysis.
    - Users: **Sales managers**, representatives, and executives.

## Dashboard Type Assessment

<img src="/assets/images/data/dash_01.webp" alt="drawing"/>

|Type of Dashboard|Examples|Characteristics |Main Users        |Platform|
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
|Executive Dashboard|CEOO Dashboard       |Viz Heavy, High Level hindsight and insights, explanatory |C-Level, SVP/VP of Business, VP/Head of functions (product, engineering, data, marketing etc), Head of Finance (FAT, FP&A, CF)|Superset|
|Financial Dashboard|Value Chain - Tracker|Table Heavy, exploratory, meticulous    |FP&A, FAT, CF, SVP/VP Business, BP representative|Superset|
|Business Performance Dashboard     |OKR Dashboard with strategic priority  |if the story board is broad enough, could possibly chunk into several Project Based dashboard|All Business, Head/Manager of Product, BP representative    |Superset by Team Data, Metabase by Non Team Data|
|Product Performance Dashboard      |Product Outcome      |User Experience Metrics Heavy, Close and Open Funnel, Digital Adoption related    |All Functions (product, engineering, data, marketing etc).  |Superset by Team Data, Metabase by Non Team Data|
|Project (Product/Operational) Based Dashboard   |Internal Fullfillment, Harvest Prediction, Supply Demand Mapping, SLA Monitoring Dashboard|End to end nit picky Dashboard that cover specific project, could possibly cover its product performance |All Functions and All Business related  |Metabase|
|Data Quality Dashboard |DQM-DG, DBS, Discrepancy, DWH Monitoring, Downstream Cost Mapping|Monitor data quality (wall of shame), is the Product, Eng and Data, Head/Manager of data consistent, any discrepancy|Product, Eng, and Data, Head/manager of bussiness  |Metabase|
|Data Platform Dashboard |Superset Usage Monitoring, Metabase RBAC|Related to data infrastructure performance         |Data   |Based on Platform       |


## How to measure the success of dashboards?

1. **Define the use cases and the audience**
you should be clear about a few things, and in particular: why you are building this dashboard and for who.
    1. **What’s the problem this dashboard is trying to solve?**
    2. **What won’t it be useful for?**
    3. **Who will be the audience of this dashboard?**
    4. **How will you know if your dashboard is a success?** 
    It can be usage-based (e.g. “more than X people connect monthly to the dashboard”) or project-based (e.g. “most project Y decision are based on data provided by the dashboard“).
2. **Benchmark // Find inspiration**
get to know your audience better and their relationship with data. 
    1. **Has our organization tried to solve this issue in the past?**
    2. **Which dashboards are popular with your audience?**
    3. **How is your audience currently doing without this dashboard?**
3. **Prototype & Build**
important to never forget that a dashboard is a tangible product that is meant to be used regularly — and the best way to make sure of that last point is to develop it with your potential users
    1. **Build mockups first.**
    running it by your potential users will allow you to make sure you are covering all of their use cases, and that the UX is ideal. Keep it simple & focused on the problem it’s trying to solve. 
    2. **Run those mockups by your potential power users.**
    Observe how they use the mockups (i.e. what are their user journeys) and if they are able to find the information they need by themselves. If they don’t or if their user journey is painful — iterate and try again.
    3. **Build the dashboard!**
4. **Test, test, test**
It means that ‘your audience is able to find the information they are looking for
    1. **Are the numbers right / do they match different data sources?
    There is nothing more damaging that having a dashboard that reports ‘wrong’ numbers — your audience may instantly losing trust .** 
    2. **Are the main user journeys working as intended?**
    identified a bunch of Critical User Journeys (CUJs)
    3. **Are the different beta testers happy with the end product?** 
    Ask your beta testers one last time for their help and let them run wild on the dashboard.
5. **Document everything**
    1. **Where is the data coming from and how is it transformed?**
    Make sure to start a product requirement document (PRD) to document where the data is coming from and which potential transformation you are applying (and why).
    2. **What are all the steps you followed to actually build this dashboard?**
    Add that to the PRD — it will be useful for the colleague who will takeover after you start working on another project.
    3. **What are some other potential considerations?**
    Use the questions from your beta testers (from step 4) to build a FAQ, and link it directly from the dashboard (potentially alongside the PRD).
6. **Release the masterpiece**
    1. **Send a launch email to all the right stakeholders.**
    2. **Consider organizing a training.**
    3. **Make sure your dashboard is discoverable.**
7. **Verify your dashboard is successful**
Did you get the # of users you expected? Is your dashboard helping the right people to do the right thing? If it doesn’t — look into what went wrong, and either fix it or learn from it. If it does — celebrate, because life is too short.