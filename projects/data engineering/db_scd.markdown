---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Database Practice - SCDs
parent: Data Engineering
permalink: /data engineering/db_scds
nav_order: 81
---

#  Database Practice
data engineering
{: .badge .badge-pill .badge-primary }
database
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}


## Slowly Changing Dimensions (SCDs)
  - are all about how you manage changes to dimensional data over time in your data warehouse or analytics system.

### Key features of slowly changing dimensions
  - Historical tracking: Handles attribute changes over time. Some SCD types preserve history (e.g., old values, change dates), while others overwrite data.
  - Natural keys: Each record is tied to a natural key. This is something that uniquely identifies a business entity and doesn’t change over time. 
  - Versioning: To keep track of when changes occur, SCDs often include metadata to track start and end dates, version numbers, or active/inactive flags. 
  - Trend analysis: By preserving historical changes, SCDs allow you to analyze trends over time.

### Types of slowly changing dimensions
  - **Type 0: Fixed attributes**
    - These are values that never change. Think of them as the constants in our data—attributes that are historically accurate and shouldn’t be updated. 
    - When to use it: For data that’s static by nature. You’re not expecting history because the data isn’t supposed to evolve.
  - **Type 1: Overwrite old values**
    - Type 1 is used when data can change, but you don’t need to keep the old values. Every time a change happens, the old value is overwritten with the new one.
    - When to use it: When current accuracy is all that matters. Use this for operational data like contact info or profile fields that change, but don’t need historical analysis.
  - **Type 2: Track full history with new rows**
    - Type 2 is your go-to tool when you want to track every change to an attribute over time. Instead of overwriting the old value, you insert a new row for each version, keeping a full history of changes. 
    - Each version has the same natural key (like product_id) but a different surrogate key (like product_version_id) and metadata like timestamps or flags to track which version is active.
    - When to use it: Ideal for slowly evolving entities like products, employees, or customer segments where you want to measure how changes affect KPIs over time.
  - **Type 3: Store limited history with extra columns**
    - Type 3 dimensions track changes in a row by adding a new column. Instead of adding a new row with a new primary key like with type 2 dimensions, the primary key remains the same, and an additional column is appended. 
    - When to use it: Use Type 3 when you only need to keep one prior version of a value, like for reference or comparison, not full historical tracking.
  - **Type 4: Separate history table**
    - Type 4 uses two tables: one for current records and one for historical records. Every time a change happens, the current table is updated, and the previous version is pushed into the history table. This keeps the current table clean and fast for queries, while still giving you a full audit trail when needed.
    - When to use it: Type 4 is great when you want to separate current vs. historical data for performance or clarity, especially in digital systems that frequently change but only analyze history occasionally.
  - **Type 6 - Hybrid**
    - Combination of types 1,2 and 3. Tracs history with current data easily.

### How to implement
  - Audit what you’ve already got
    - What dimension tables already exist?
    - Are any of them changing over time?
    - Do any require historical tracking?
  - Prioritize the problem areas
  - Choose the right SCD types
    - Frequency of change: Does the data change often or rarely?
    - Need for history: Is there a business need to analyze historical values, or do you only care about the current state?
    - Analytical requirements: Do you need a complete history, or just a flag for "previous" vs. "current" versions?
  - Decide how to handle legacy data
    - Option 1: Start fresh: This involves acknowledging that historical data prior to your implementation date will not have SCD tracking. 
    - Option 2: Backfill: If business requirements absolutely demand a complete history, you can attempt to backfill. This often requires complex logic to rebuild timelines from available snapshots or audit logs. 
  - Implement logic in the data pipelines
    - Detect changes
    - Include critical metadata


