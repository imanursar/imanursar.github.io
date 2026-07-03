---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Database Practice
parent: Data Engineering
permalink: /data engineering/db_norm
nav_order: 80
---

#  Database Practice
data engineering
{: .badge .badge-pill .badge-primary }
database
{: .badge .badge-pill .badge-secondary }


## Database Normalization

  - **1NF - First Normal Form**
    - Eliminate repeating groups
    - Rules:
      - Each column must have atomic (unit) values.
      - No repeating groups or arrays.
    - Example:
      - there is no row with aggregate value.

      |ID |Name         | Phone    |
      |--:|------------:|:---------|
      | 1 | Alice       | 987      |
      | 2 | Alice       | 864      |
      | 3 | Bob         | 432      |
      | 4 | Charles     | 431      |
      | 5 | Charles     | 646      |

  - **2NF - Second Normal Form**
    - Remove partial dependencies
    - Rules:
      - Must be in 1NF.
      - Every non-key attribute must be fully functionally dependent on the whole primary key.
    - Example:

      |OrderID  | OrderDate       |
      |--------:|:----------------|
      | 101     | 2024-01-01      |
      | 102     | 2024-02-06      |
      | 103     | 2025-04-09      |
      | 120     | 2025-09-11      |
      | 110     | 2026-12-12      |

      |OrderID |ProductID| ProductName    | Price |
      |-------:|--------:|:---------------|:------|
      | 101    | 1       | Pen            | 10    |
      | 101    | 2       | Book           | 20    |
      | 102    | 1       | Pen            | 10    |

  - **3NF - Third Normal Form**
    - Remove transitive dependencies
    - Rules:
      - Must be in 2NF.
      - No transitive dependency. Non-key attributes should not depend on other non-key attributes.
    - Example:

      |EmpID |EmpName| DeptID |
      |-----:|------:|:-------|
      | 101  | Alice | 10     |
      | 102  | Bob   | 20     |
      | 103  | Charles| 10    |

      |DeptID  | DeptName        |
      |-------:|:----------------|
      | 10     | HR              |
      | 20     | IT              |

  - **BCNF - Boyce-Codd Normal**
    - Rules:
      - Must be in 3NF.
      - For every functional dependency X -> Y, X must be a super key.
    - Example:

      |DeptID  | Sub-Dept        |
      |-------:|:----------------|
      | 10     | Data            |
      | 10     | IT              |

      |Sub-Dept |name   |
      |--------:|------:|
      | Data    | Alice |
      | Data    | Bob   |
      | IT      | Charles|

  - **4NF - Forth Normal Form**
    - Remove multi-valued dependencies
    - Rules:
      - Must be in BCNF.
      - No no-trivial multi-valued dependencies.
    - Example:

      |EmpID |EmpName|
      |-----:|------:|
      | 101  | Alice |
      | 102  | Bob   |
      | 103  | Charles|

      |EmpID    | DeptName        |
      |--------:|:----------------|
      | 101     | HR              |
      | 102     | IT              |
      | 103     | IT              |

  - **5NF - Fifth Normal Form**
    - Remove join dependencies
    - Rules:
      - Must be in 4NF.
      - No join dependencies. Every fact must be represented in one table only.
    - Example:

      |EmpID |EmpName|
      |-----:|------:|
      | 101  | Alice |
      | 102  | Bob   |
      | 103  | Charles|

      |EmpName  | DeptName        |
      |--------:|:----------------|
      | Alice     | HR              |
      | Bob     | IT              |
      | Charles  | IT              |

      |DeptName| Sub-DeptName    |
      |-------:|:----------------|
      | HR     | GA              |
      | IT     | Infra           |
      | IT     | Software        |

---

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

# Technique
  - ETL
  - Change data capture: Real-time processing
  - Tracking history with effective dates
  - 


