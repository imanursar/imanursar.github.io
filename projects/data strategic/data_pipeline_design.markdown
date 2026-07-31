---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Data Pipeline Design Patterns
parent: Data Strategic
permalink: /data strategic/pipeline
nav_order: 88
---

# Data Pipeline Design Patterns

data pipeline
{: .badge .badge-pill .badge-primary }
data strategic
{: .badge .badge-pill .badge-secondary }


## Main Designs
  - Raw Data Load
  - ETL
  - Reverse ETL
  - ELT
  - EtLT
  - Data Virtualization
  - Streaming Pipelines
  - Lambda Architecture
  - kappa Architecture
  - Data Mesh 
  - Data Lakehouse

## Schema
  {% include whimsical.html src="https://whimsical.com/embed/JSC42FRTDvPy9vcbdQRpaG@or4CdLRbgrohYymNukERVEFQiwoif8SMbUkhPoBGi?color-mode=system" %}

## Data Pipeline
  A data pipeline moves data from sources through transformations to destinations reliably, at scale, and on schedule. For ML engineers, pipelines are the backbone of every training, serving, and monitoring system. 

## Key Concepts

  | Concept             | Description                                                                                                                                                       |
  | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | Data Pipeline       | A series of processing steps that move and transform data from source to destination. Automated, monitored, repeatable.                                           |
  | ETL vs ELT          | ETL: Extract → Transform → Load (transform before storing). ELT: Extract → Load → Transform (transform in the warehouse). ELT dominates modern cloud data stacks. |
  | Batch Processing    | Process accumulated data at scheduled intervals (hourly, daily). High throughput, simple, tolerates latency. Tools: Spark, Airflow, dbt.                          |
  | Stream Processing   | Process events as they arrive, millisecond to second latency. Complex but real-time. Tools: Kafka, Flink, Spark Structured Streaming.                             |
  | Lambda Architecture | Hybrid: batch layer (accurate, slow) + speed layer (approximate, fast) + serving layer. Complex to maintain but handles both.                                     |
  | Kappa Architecture  | Stream-only: everything is a stream, replay for reprocessing. Simpler than Lambda. Preferred when stream processing is fast enough.                               |
  | Idempotency         | Processing the same data multiple times produces the same result. Critical for safe retries. Design every pipeline step to be idempotent.                         |
  | Backfill            | Re-processing historical data with a new pipeline or corrected logic. Airflow and Spark both support parameterised backfill runs.                                 |

## Decision for pipeline
  
  | Decision               | Criteria                                                                                                                  |
  | ---------------------- | ------------------------------------------------------------------------------------------------------------------------- |
  | **Use Batch when**     | Latency of hours/days acceptable · Large volumes per run · Existing data warehouse · ML training pipelines · BI reporting |
  | **Use Streaming when** | Real-time decisions needed · Fraud detection · Live ML predictions · User-facing dashboards · Event-driven alerting       |
  | **Use Lambda when**    | Need both: accurate historical analysis + real-time approximation · High-traffic recommendation systems                   |

## Tools
  - **Apache Airflow — Orchestration Engine**
    - Airflow is the industry-standard pipeline orchestrator. It defines, schedules, and monitors workflows as Directed Acyclic Graphs (DAGs). Every ML training pipeline, data ingestion job, and model deployment workflow can be expressed as an Airflow DAG. 
  
    <img src="/assets/images/data/data_strategic/data_pipeline/dsdp_01.webp" alt="drawing"/>

  - **Apache Kafka — Distributed Event Streaming**
    - Kafka is a distributed event streaming platform built for high-throughput, fault-tolerant, real-time data pipelines. It is the backbone of most production ML serving systems that need to process events as they happen. 
  
    <img src="/assets/images/data/data_strategic/data_pipeline/dsdp_02.webp" alt="drawing"/>

  - **Apache Spark — Large-Scale Data Processing**
    - Spark is the dominant large-scale data processing engine. It processes data in-memory across a cluster, supports SQL, ML (MLlib), streaming, and graph processing — all with a unified API in Python (PySpark), Scala, or Java. 

    <img src="/assets/images/data/data_strategic/data_pipeline/dsdp_03.webp" alt="drawing"/>





