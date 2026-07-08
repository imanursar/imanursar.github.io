---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Data Architecture
parent: Data Strategic
permalink: /data strategic/data_arch
nav_order: 120
---

# Data Architecture

data architecture
{: .badge .badge-pill .badge-primary }
data government
{: .badge .badge-pill .badge-secondary }
data management
{: .badge .badge-pill .badge-info }



## Definition
Data architecture provides a structured framework for organizing and managing an organization's data assets. It defines how data is collected, stored, transformed, and used to meet business needs while adhering to data governance standards and policies.

## Problems To Solve by Data Architecture
- **System Incompatibilities**: Existing systems may be outdated and unable to work together, hindering data access and analysis.
- **Compliance Risks**: Lack of proper data governance practices can lead to regulatory violations and fines.
- **Data Discoverability**: Users struggle to find the data they need or may be using outdated information, leading to poor decision-making.
- **High Costs**: Inefficient data storage and processing result in unnecessary expenses.
- Operational Inefficiency: Simple data management tasks take too long, hindering productivity and slowing down analysis.
- **Security Vulnerabilities**: A lack of security measures and data masking exposes sensitive information to unauthorized access and potential breaches.

## Goals of Successful Data Architecture
- **Automation**: Automate repetitive tasks and processes to improve efficiency and free up resources.
- **Cost Optimization**: Reduce operational costs by optimizing resource usage and licensing fees.
- **Simplified Maintenance**: Make it easy for all team members to add new data sources and maintain the system.
- **Strong Covernance**: Ensure compliance with all regulations and enable root cause analysis through clear data lineage.

## Fundamentals
- **Extensibility**
  - **Modular / Reusability**: Design reusable components and templates for common tasks like data ingestion and transformation. 
    - Example: All data ingestion pipelines are created from a standardized template.
  - **Pluggability**
- **Agility**
  - **Deployability**
    - Installability
    - Upgradeability
    - Portability
  - **Configurability**
    - Compatibility
  - **Maintainability**
    - Testability
    - Ease to development
- **Scalability**
  - **Traffic Pattern**
    - Diurnal Pattern: **predictable, cyclical variations in traffic volume** that occur over a 24-hour period, typically characterized by high traffic during working hours and low traffic at night. This gradual rise and fall allows systems to adapt through auto-scaling and standard load balancing, as the increase in demand is smooth and foreseeable.
    - Thundering Herd: is not about total volume but about synchronized, simultaneous access to a shared resource by a large number of clients or processes. This occurs when **traffic spikes in a sudden, coordinated burst** (e.g., cache expiration, flash sales, or retry storms) rather than gradually. 
      - Peak time
      - Densely Populated Area
- **Metadata Management**: Establish a system to define and maintain metadata for all datasets, ensuring data is easily discoverable and understood.
  - Example: Automatically register target tables in a data catalog.
- **Data Governance**: Implement data standards and policies to ensure data quality, consistency, and compliance.
  - Example: Enforce data contracts on all output tables and validate data against those contracts.
  - **Consistency**
    - Data Freshness
  - **Usability**
    - API Contract
    - Learnability
    - Accessability
  - **Availablility**
    - Deployment Stamps: enhances availability by partitioning a platform into multiple, independent, and identical units (stamps) that contain full copies of the application stack, including compute, storage, and networking. This architecture ensures that a failure in one stamp does not affect others, limiting the blast radius and allowing for 99.99%+ availability when combined with multi-Availability Zone deployments.
    - Geodes: ensures high data availability by deploying backend services into multiple geographically distributed nodes, known as geodes, which operate in an active-active style.
  - **Observeability**
    - Alerts and Monitoring
    - L1 / L2 / L3: In general infrastructure and data observability, these levels denote the scope of monitoring. 
      - L1 (Edge/Network): Focuses on ingress, latency, and packet errors. 
      - L2 (Service/Application): Tracks request flows, errors, and business events. 
      - L3 (Data/Storage): Monitors query performance and throughput within data warehouses.
    - Logging
- **Migration Planning**: Analyze existing systems, identify risks, and create a plan for migrating to the new architecture. 
  - Example: Convert existing ETL jobs into modern, metadata-driven data pipelines.
- **Security**
  - **Auditability**
  - **Legality**
    - Compliance
    - Privacy
    - Certifications
  - **Authentication and Authorization**
    - MFA
- **Durability**
  - **Replication**
  - **Fault Tolerance**
  - **Archivability**
- **Resiliency**
  - **Recoverability**
    - Disaster Recovery
  - **Design Pattern**
    - Bulkhead: Prevent one leaking compartment from sinking the whole ship. 
      - Example: The low process ETL suddenly consumes all CPU, everything becomes slow. 
      - With Bulkhead, Reserve resources for each process.
    - Circuit Breaker: Stop repeatedly trying a broken engine.
      - Example: a fail process will create repeat retry process that will lead to shutdown process. If healthy: Resume work.
      - With Circuit Breaker, after repeated failures, stop sending requests. Wait. 
    - Leader Election: Decide which captain is in charge.
      - Example: Imagine three schedulers, without leader election. All three execute: Data loads three times. Leads to duplicates.
      - With Leader Election, each process will be queue for become leader and execute it process.

## Layers
- **Data Ingestion**: Define how data in different formats (batch, streaming) is acquired and initially stored. 
  - Example: Incoming files are organized in date-partitioned folders within cloud storage.
- **Data Transformation**: Design and test standardized templates for data transformation processes.
  - Example: Standardize data cleansing and transformation using a pipeline template.
- **Data Storage**: Determine the appropriate storage solutions for raw, processed, and published data, considering cost, security, and performance 
  - Example: Use Snowflake as the data warehouse solution.
- **Data Publishing**: Define how users and applications access the data they need.
  - Example: Provide data analysts with a SQL endpoint to access data for analysis and reporting.

## Maintenance
- **Monitoring**: Decide how to monitor pipelines, infrastructure, and data quality to ensure system health and identify issues. 
  - Example: Set up alerts for pipeline failures and data quality violations.
- **Incident Management**: Define clear roles, responsibilities, and workflows for handling and escalating incidents. 
  - Example: Automatically generate support tickets for critical data quality issues and pipeline failures
- **Deployment**: Plan and manage the deployment of data architecture components across the infrastructure. 
  - Example: Use a CI/CD pipeline to automate the deployment of updates to data processing applications.
- **Data Quality**: Implement data quality checks within pipelines and establish ongoing data quality testing procedures. 
  - Example: Include schema validation and completeness checks in data ingestion pipelines.

## Types of data architecture
- Centralized
  - Data brought into one main platform.
  - single governance model
  - strong consistancy and reporting
- Decentralized
  - ownership spread across domains and teams.
  - local schemas, metadata, and access rules.
  - good for outonomy and speed.
- Hybrid
  - blend of centralized and decentralized.
  - balance scale, integration, and agility.
  - common modern approach.

## Types of data models
- Conceptual
- Logical
- Physical

