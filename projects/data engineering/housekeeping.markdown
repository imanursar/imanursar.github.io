---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Housekeeping for intermediate data
parent: Data Engineering
permalink: /data engineering/hk
nav_order: 106
---

#  Housekeeping
data engineering
{: .badge .badge-pill .badge-primary }
intermediate
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

# Housekeeping Guideline
  ETL housekeeping defines how temporary data, intermediate files, memory objects, sessions, and archived outputs are created, managed, retained, compressed, and removed during data processing.

  The objective is to prevent temporary processing artifacts from becoming permanent data assets.

  Housekeeping must answer five questions for every ETL process:
  - Where is temporary data created?
  - How long does it need to exist?
  - What happens when processing succeeds?
  - What happens when processing fails?
  - When and how is the temporary data removed or archived?

  The default principle is:
  > Temporary data must have an explicit lifecycle. No temporary data should exist indefinitely without a documented business or technical reason.

## Core lifecycle
  1. A standard ETL temporary-data lifecycle
  ```mermaid
  Create
    ↓
  Generate / Process
    ↓
  Validate
    ↓
  Consume / Publish
    ↓
  Cleanup
    ↓
  Verify Cleanup
  ```
    
  2. For data that needs to be retained
  ```mermaid
  Create
    ↓
  Generate / Process
    ↓
  Validate
    ↓
  Compress
    ↓
  Archive
    ↓
  Apply Retention Policy
    ↓
  Delete After Retention
  ```

  3. For memory-based processing:
  ```mermaid
  Allocate Memory
    ↓
  Process Data
    ↓
  Release Objects
    ↓
  Garbage Collection
    ↓
  Verify Memory Release
  ```

## Data Classification

  | Type                 | Example                          | Expected Process                        |
  | -------------------- | -------------------------------- | --------------------------------------- |
  | Temporary file       | CSV, JSON, Parquet               | Delete after successful processing      |
  | Temporary directory  | `/tmp/etl/customer_001/`         | Delete after process completion         |
  | Staging table        | `stg_sales_daily`                | Truncate/drop after processing          |
  | Intermediate table   | `tmp_customer_aggregation`       | Delete after downstream consumption     |
  | Memory object        | DataFrame                        | Release after processing                |
  | Failed-run artifacts | Partial output                   | Retain temporarily for debugging        |
  | Archive              | Historical raw/intermediate data | Compress and retain according to policy |
  | Checkpoint           | ETL restart state                | Retain until pipeline completion        |
  | Cache                | API/query/cache result           | TTL-based expiration                    |

## Schemas
### Schema 1 — Replace Temporary Area
  Use this pattern when the temporary area represents the current processing state and does not need to preserve the previous run. Able to create multiple temporary area. 

  This schema is needs for:
  - Only the latest data is required.
  - The next process consumes the same location.
  - Historical temp data has no business value.
  - Reprocessing can regenerate the data.
  - Storage needs to be controlled.
  - Potentially to examine the temp data.

  Risk:
  - If the previous data is removed before the new process succeeds, a failed run can leave the downstream process without usable data.

  ```mermaid
              Check Temporary Area / Staging Table
                      ↓
              Create if Not Exists
                      ↓
              Replace / Clean Existing Contents
                      ↓
                  Validate
                      ↓
              Generate Data
                      ↓
              Validate Data
                      ↓
              Finish Processing
                      ↓
      ┌───────────────┴───────────────┐
      ↓                               ↓
      Keep for Next Process          Dump
                                      ↓
                                  Compress
                                      ↓
                                  Archive
  ```

### Schema 2 — Create, Process, Delete
  Use this pattern when temporary data exists only during a single ETL execution.

  This schema is needs for:
  - Data has no value after processing.
  - The next process does not require the files.
  - Temp files are large.
  - The pipeline runs frequently.
  - Storage cost is significant.

  Risk:
  - Cleanup must happen even when the ETL fails.
  - Potentially delete failed-run artifacts and lost capable to troubleshooting.

  ```mermaid
      Create Temporary Area / Staging Table
              ↓
      Generate Data
              ↓
      Write Data
              ↓
      Process / Consume Data
              ↓
      Validate
              ↓
      Finish
              ↓
      Delete Temporary Data
              ↓
      Verify Deletion
  ```

### Schema 3 — In-Memory Processing
  Use this when the ETL does not write intermediate data to persistent storage. Keep in mind that some programs using a reference to allocate the memory that can prevent the object/data from being released.

  ```mermaid
      Check Memory
          ↓
      Allocate Data Objects
          ↓
      Generate / Transform Data
          ↓
      Consume Data
          ↓
      Release Data
          ↓
      Garbage Collection
          ↓
      Verify Memory
  ```

### Schema 4 — Streaming Processing
  1. **Cleanup Policy**: A cleanup policy defines how a topic manages messages that are no longer required, whether they are deleted or retained in a more compact form. This mechanism is essential for controlling storage usage and maintaining data relevance over time.
  - Types of cleanup policies:
    - **Delete**: Messages are automatically removed once they exceed defined retention thresholds, such as time or storage size (cleanup.policy=delete).
    - **Compact**: Messages are retained based on their key, with older records being compacted so that only the latest value for each key is preserved (cleanup.policy=compact).
  2. **Retention**: defines how long messages remain available within a topic before they are eligible for deletion. It provides control over data lifecycle, ensuring storage is managed efficiently while preserving data for an appropriate duration.
  - Retention types:
    - **Time-based retention**: Messages are removed once they exceed a specified time window (e.g., retention.ms=604800000, which corresponds to 7 days).
    - **Size-based retention**: Messages are deleted when the total size of the topic surpasses a defined limit (e.g., retention.bytes=1073741824, or 1 GB).

## Failure-Aware Housekeeping
  A Housekeeping process should distinguish between successful and failed executions. Each process should manages the temporary data differently. Either with replace, delete, or compress and delete.

  ```mermaid
                  Start
                    ↓
              Create Area
                    ↓
                Process
                    ↓
              Validate Output
              /           \
            Success        Failure
              ↓              ↓
          Publish       Mark Failed
              ↓              ↓
          Cleanup       Retain Debug
              ↓              ↓
          Complete       TTL Cleanup
  ```

## Retention status and policy
  - **How to setup the Retention status**

    | Execution Status | Temporary Data                           |
    | ---------------- | ---------------------------------------- |
    | Success          | Delete immediately                       |
    | Failed           | Retain temporarily                       |
    | Cancelled        | Retain temporarily                       |
    | Partial success  | Retain according to recovery requirement |
    | Debug run        | Explicit retention                       |
    | Archived         | Move/compress before deletion            |

  - **How to classify the retention policy**

    | Class | Example                 |                          Retention |
    | ----- | ----------------------- | ---------------------------------: |
    | T0    | Disposable intermediate |                 Immediate deletion |
    | T1    | Failed-run debugging    |                           24 hours |
    | T2    | Recovery/checkpoint     |          Until pipeline completion |
    | T3    | Operational archive     |                          7–30 days |
    | T4    | Business archive        |         Defined by business policy |
    | T5    | Regulatory/audit        | Defined by legal/compliance policy |

  The exact duration must be determined by the business and data owner. Engineering should not invent regulatory retention periods.

## Special process for database-based ETL
  For database-based ETL, it recommended to use:
  - Use TRUNCATE when the staging structure will be reused.
  - Use DROP when the staging object itself is temporary and has no reason to remain.
  - Config the locking, logs, indexes, partitions, etc.

## Principles
  Temporary Process and storage must have:
  - A defined ownership and lifecycle.
  - Storage naming
  - Name Conversion
  - Versioning
  - Compress and Archive
  - Housekeeping Monitoring matrics
  - Idempotency (should behave correctly if called twice)
  - Concurrency (must not delete data belonging to an active process)

# Template Documentation
  The current ETL process generates temporary files during daily processing. 
  These files remain in the processing server after the ETL completes, causing unnecessary storage consumption and increasing operational risk.

  The objective is to establish an automated process for temporary data and remove temporary artifacts after successful processing.

  This documentation can tell about how we treat temporary data from ETL process. Either the data in storage or in memory. Refer this table and it flow to determine how the ETL handle the temporary data and how it manage to housekeeping in storage.


  | Field                                     | Value                                    |
  | ------------------------------------------| ---------------------------------------- |
  | Storage path                              | /data/etl/temp/customer/                 |
  | Storage name                              | temp_20261010_geoai_data                 |
  | Data Process                              | GEOAI Data Pipeline                      |
  | Pipeline Name                             | Inferencing result                       |
  | Versioning                                | [NONE, by date, by version]              |
  | Access                                    | Admin                                    |
  | Maximum Expected Size / memory usage      | 5 GB                                     |
  | What happens when memory is insufficient  | The process will fail                    |
  | Retention                                 | Schema 1 (explain what schema 1 is)      |
  | Monitoring                                | Storage utilization > 80%                |
  | Compression and Archive (explain with 5W1H)| NO / YES                                |

  *This is a template that can be customized based on the project’s needs.
