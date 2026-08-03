---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Data Warehouse 101
parent: Data Strategic
permalink: /data strategic/warehouse_101
nav_order: 90
---

# Data Warehouse 101
data Strategic
{: .badge .badge-pill .badge-primary }
data warehouse
{: .badge .badge-pill .badge-secondary }
design patterns
{: .badge .badge-pill .badge-info }


## What is a Data Warehouse?
  A centralized repository of integrated data from multiple sources, structured for query and analysis rather than transaction processing.

### Key Characteristics
  - **Subject-oriented**: Focused on business subjects like sales, marketing
  - **Integrated**: Consistent naming, measurement, encoding
  - **Time-variant**: Historical data for trend analysis
  - **Non-volatile**: Data is stable and read-only

  <img src="/assets/images/data/data_strategic/data_warehouse/ware_01.webp" alt="drawing"/>

## OLTP vs OLAP

  | Dimension       | OLTP Online Transaction Processing        | OLAP Online Analytical Processing       |
  | --------------- | ----------------------------------------- | --------------------------------------- |
  | Purpose         | Operational tasks, transaction processing | Business intelligence, decision support |
  | Data Structure  | Normalized, entity-relationship model     | Denormalized, star/snowflake schema     |
  | Users           | Front-line workers, clerks, cashiers      | Knowledge workers, analysts, managers   |
  | Operations      | Simple, read/write operations             | Complex, read-only queries              |
  | Response Time   | Milliseconds - immediate                  | Seconds to minutes - analytical         |
  | Database Design | Application-oriented                      | Subject-oriented                        |
  | Data Volume     | GBs of current data                       | TBs to PBs of historical data           |
  | Examples        | ATM, Order entry, POS systems             | Financial analysis, sales forecasting   |

## Data Warehouse Architecture

### Data Warehouse Components

  - Components
    - Source Systems
    - ETL/ELT
    - Staging Area
    - Data Warehouse
    - Data Marts

  | Dimension       | Traditional Architecture                  | Modern Architecture                     |
  | --------------- | ----------------------------------------- | --------------------------------------- |
  | Processing      | ETL (Extract, Transform, Load)            | ELT (Extract, Load, Transform)          |
  | Storage         | On-premise hardware                       | Cloud-native services                   |
  | Data Model      | Structured schemas                        | Flexible (structured + semi)            |
  | Updates         | Batch processing                          | Real-time streaming                     |
  | Access          | Limited to BI tools                       | Multiple interfaces (APIS, SQL)         |

### Data Warehouse schema types
  - **Star Schema**
    - Central fact table with dimension tables
    - Denormalized dimension tables 
    - Simple structure, fast queries
    - Best for Simple analytics

    - <img src="/assets/images/data/data_strategic/data_warehouse/ware_02.webp" alt="drawing"/>

  - **Snowflake Schema**
    - Normalized dimension tables
    - Reduced redundancy, complex structure
    - Better for maintenance
    - Best for Complex dimensions

    - <img src="/assets/images/data/data_strategic/data_warehouse/ware_03.webp" alt="drawing"/>
    
  - **Galaxy Schema**
    - Multiple fact tables sharing dimensions 
    - Supports complex business models 
    - Also called Fact Constellation
    - Best for Enterprise-wide

    - <img src="/assets/images/data/data_strategic/data_warehouse/ware_04.webp" alt="drawing"/>

### Fact Table Types
  - **Transactional Fact Table**
    - Records individual transactions
    - Captures at the lowest grain
    - Most common fact table type

    - <img src="/assets/images/data/data_strategic/data_warehouse/ware_06.webp" alt="drawing"/>

  - **Periodic Snapshot Fact Table**
    - Captures state at regular intervals 
    - Contains semi-additive measures 
    - Good for trend analysis

    - <img src="/assets/images/data/data_strategic/data_warehouse/ware_07.webp" alt="drawing"/>
    
  - **Accumulating Snapshot Fact Table**
    - Tracks process milestones
    - One row per business process 
    - Updated as process evolves

    - <img src="/assets/images/data/data_strategic/data_warehouse/ware_08.webp" alt="drawing"/>

  <img src="/assets/images/data/data_strategic/data_warehouse/ware_05.webp" alt="drawing"/>

### Slowly Changing Dimensions (SCD) Types

  [SCD will discuss here](https://imanursar.github.io/data engineering/db_scds)

## ETL vs ELT

  **ETL (Extract - Transform - Load)**

  - Key Characteristics
    - Transforms data before loading
    - Processing in separate server
    - Better for complex transformations
  - ETL Preferred
    - Complex transformations before loading
    - Legacy systems integration
    - Strict data quality requirements
    - Regulatory compliance needs


  **ELT (Extract - Load - Transform)**

  - Key Characteristics
    - Transforms data after loading
    - Processing in target system
    - Better for large datasets
  - ELT Preferred
    - Big data volumes processing
    - Cloud-native environments
    - Real-time data needs
    - Flexible analytics requirements

  **Hybrid Approach**

  - Mixed environments (on-prem + cloud)
  - Multiple data types (structured + unstructured)
  - Migration scenarios (gradual transition)
  - Complex data pipelines with varied needs

## Data Processing Concepts

  - **Data Pipelines**
    - Orchestrated data flow
    - Automated data movement
    - Components: Extract, Transform, Load
    - Schema:
      - Batch: Scheduled processing
      - Streaming: Real-time processing
      - Micro-batch: Small frequent batches

  - **Batch vs Real-time Processing**
    - Batch processing
      - High throughput
      - Lower cost
      - Complex transformations
    - Real-time Processing
      - Low latency
      - Immediate insights
      - Event-driven

  - **Lambda & Kappa Architecture**
    - Lambda
      - Dual paths: batch + speed layer
      - Lambda: Complex, fault-tolerant
    - Kappa
      - Single path: streaming only
      - Kappa: Simpler, unified processing
  
  - **Data Ingestion Methods**
    - Push-based: Source sends data
    - Pull-based: Destination fetches data
    - Change Data Capture: Tracks changes
    - API-based: REST/GraphQL endpoints

## Data Quality & Governance

  - **Data Profiling**
    - Data assessment
    - Analyzing data to discover content, structure, and relationships to identify quality issues
  - **Data Validation**
    - Quality assurance
    - Ensuring data meets business rules and requirements through automated checks
  - **Data Cleansing**
    - Error correction
    - Correcting or removing or inaccurate, incomplete, or inconsistent data
  - **Metadata Management**
    - Data documentation
    - Data Managing about data, to provide context, meaning, and usability
  - **Data Lineage**
    - Data provenance
    - Tracking data origin, movement, and transformation throughout its lifecycle
  - **Master Data Management**
    - Data consistency
    - Creating a single source of truth for criticalbusiness data

## Storage & Query Optimization

  - **Partitioning**
    - Faster query scans
    - Dividing large tables into smaller, manageable parts based on specific criteria
  - **Columnar Storage**
    - Ideal for aggregation queries that access few columns across many rows
    - Storing data by column rather than row to improve analytical query performance
  - **Indexing**
    - Reduced I/O operations
    - Creating data structures for faster data retrieval without scanning entire tables
  - **Query Pushdown**
    - Minimized network overhead
    - Moving computation closer to data to reduce data transfer and improve performance
  - **Materialized Views**
    - Instant complex queries
    - Pre-computed query results stored as physical objects for faster access

## Performance Tuning Concepts

  - **Caching**
    - Store frequently accessed data in memory
    - Result set and metadata caching
    - Automatic cache invalidation
    - 10-100x faster queries
  - **Clustering**
    - Physically organize data based on query patterns
    - Co-locate related data together
    - Automatic re-clustering maintenance
    - Reduced I/O operations
  - **Compute Scaling**
    - Adjust resources based on workload
    - Vertical scaling (bigger nodes)
    - Horizontal scaling (more nodes)
    - Cost-performance balance
  - **Query Execution Plans**
    - Visualize query processing steps
    - Identify bottlenecks and inefficiencies
    - Cost-based optimization
    - Strategic query optimization

## Modern Data Architecture Trends
  - **Lakehouse Architecture**
    - combines data lake & warehouse
    - Single copy of data for multiple uses
    - Supports BI & ML workloads
  - **Delta Lake**
    - Brings ACID transactions to data lakes
    - Time travel & version control
    - Handles streaming & batch workloads
  - **Fabric Warehouse**
    - Microsoft's unified analytics platform
    - Integrates Power BI, Synapse, Data Factory
    - OneLake for all data

## Emerging Data Architecture Patterns
  - **Data Mesh**
    - Decentralized data ownership
    - Domain-oriented data products
    - Self-serve data platform
  - **Medallion Architecture**
    - Bronze: Raw data layer
    - Silver: Cleansed & validated
    - Gold: Business-ready tables
  - **Reverse ETL**
    - oves processed data back to operational systems
    - Enables actionable insights in business tools
    - Creates data-driven workflows


