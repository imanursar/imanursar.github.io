---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Data Design Pattern
parent: Data Strategic
permalink: /data strategic/ddp
nav_order: 85
---

# Data Design Pattern

data design
{: .badge .badge-pill .badge-primary }
data strategic
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

# Schema

  {% include whimsical.html src="https://whimsical.com/embed/JSC42FRTDvPy9vcbdQRpaG@8ADn3nfZACarxeMf2a56uqYni4ZFxNUNM3yH" %}

# Data Ingestion Design Patterns
## Full Load 
### Pass-through Jobs
  Extract and load (EL). It uses native data stores commands to export data from one database and import it to another.

  If we need to load the data between heterogeneous databases, we will need to adapt the input format to the output format with a thin transformation layer between the extract and load steps. Our pipeline then becomes an extract, transform, load (ETL) job.

  The Full Loader’s implementations will often be batch jobs running on some regular schedule.

  - **Consequences**
    - Data volume
      - if the loaded dataset grows slowly or spontaneously.
      - add auto-scaling capabilities.
    - Data consistency
      - The data may be completely overwritten, expecially when we tempted to fully replace it in each run with a drop-and-insert operation.
      - During the ingestion process, it will distrupt data availability.
      - We may need to use the previous version of the dataset if unexpected issues arise.

  - **Example**
    - Script and deploy it to our runtime service
    - Apache Spark and Delta lake: read and write API to write JSON records

## Incremental Load
  ingest smaller parts of a physically or logically divided dataset, often at a higher frequency.
### Incremental Loader
  Processes new parts of the dataset, thus its name, the Incremental Loader.

  - **Implementation**
    - **Delta column**: to identify rows added since the last run. the delta column implementation needs to remember the last ingestion time value to incrementally process new rows.
    - **Time-partitioned datasets**: the ingestion job uses time-based partitions to detect the whole new bunch of records to ingest.

    <img src="/assets/images/data/data_pattern/data_pattern_01.webp" alt="drawing"/>

  - **Consequences**
    - Hard deletes
      - Using the pattern can be tricky for mutable data. Specifically for updated and deleted process. Where if deletes a row, the information physically disappears from the input dataset. To overcome this issue we can rely on soft deletes, where the producer, instead of physically removing the data, simply marks it as removed. Put differently, it uses the `UPDATE` operation instead of `DELETE`.
    - Backfilling
      - To prevent changing between increment process to full load process due to backfilling, we could `limiting the ingestion window`. 
      - This operation brings two things: 
        - Better control over the data volume
        - Simultaneous ingestion.

  - **Example**
    - Script, applies to the incremental load and deploy it to our runtime service
    - Apache Airflow and Apache Spark: Using File Sensor and once the partition is ready, the pipeline triggers the data ingestion job.

### Change Data Capture
  This pattern has better for a lower ingestion latency or built-in support for the physical deletes.

  The latency requirement makes it impossible to use the Incremental Loader. The pattern has some job scheduling and query execution overheads that could make the expected latency difficult to reach. A better candidate is the Change Data Capture (CDC) pattern. Due to its internal ingestion mechanism, it guarantees lower latency. The pattern consists of continuously ingesting all modified rows directly from the internal database commit log. It allows lower-level and faster access to the records, compared to any high-level query or processing task.

  A commit log is an append-only structure. It records any operations on the existing rows at the end of the logfile. The CDC consumer streams those changes and sends them to the streaming broker or any other configured output. From that point on, consumers can do whatever they want with the data, such as storing the whole history of changes or keeping the most recent value for each row.

  Besides guaranteeing lower latency, CDC intercepts all types of data operations, including hard deletes. So there is no need to ask data producers to use soft deletes for data removal.

  - **Consequences**
    - Complexity
      - The CDC pattern may need some help from the operations team, for example, to enable the commit log on the servers.
    - Data scope
    - Payload
      - CDC will bring additional metadata with the records, such as the operation type (update, insert, delete), modification time, or column type.
    - Data semantics
      - Data in motion has different processing semantics for many operations that appear to be trivial in the data-at-rest world.
      - Example: when joining 2 data with or without streaming source, there will be some issues mainly in delay process.

  - **Example**
    - Create our own commit log reader
    - Debezium + Kafka Connect

## Replication
  The main goal of which is to copy data as is from one location to another. Replication is about moving data between the same type of storage and ideally preserving all its metadata attributes, such as primary keys in a database or event positions in a streaming broker.
### Passthrough Replicator
  Similar with pass-through job expecially in separate environments e.g.: development, staging, and production.

  - **Implementation level**
    - **The compute level** implementation relies on the EL job, which is a process with only two phases, read and write. Ideally, the EL job will copy files or rows from the input as is (i.e., without any data transformation).
    - **The infrastructure level** part is based on a replication policy document where we configure the input and output location and let our data storage provider replicate the records on our behalf.

  - **Consequences**
    - Keep it simple
      - The main goal is get the data as is. To reduce the interference risk in the replicated dataset, we should rely on the simplest replication job possible, which is ideally the data copy command available in the database.
      - Use the simpler raw text API that will take and copy lines as they are, without any prior interpretation.
    - Security and isolation
      - implement the replication with the push approach instead of pull to manage risk such as stability issue.
      - Push apporach means that the environment owning the dataset will copy it to the others and thus control the process with its frequency and throughput.
      - PII data
        - Use the Transformation Replicator pattern that adds an extra transformation step to get rid of any unexpected attributes.
      - Latency
        - The infrastructure-based implementation often has some extra latency, and we should always check the service level agreement (SLA).
      - Metadata

  - **Example**
    - Using Distributed data processing framework 
    - A data copy utility script running on our storage layer
    - Apache Spark: synchronize semi-structured JSON files
    - Apache Kafka: requires an extra ordering guarantee within the partitions.
    - the infrastructure-based: MirrorMaker utility for topic replication, replication mechanism tools (e.g. Terraform).

### Transformation Replicator
  Performing tests against real data to avoid surprises during production. We can’t use a synthetic data generator because our data provider often has data quality issues and it’s impossible to simulate them with any tool. We have to replicate the data from production to the staging environment. Unfortunately, the replicated dataset contains PII data that is not accessible outside the production environment.

  We should implement the Transformation Replicator pattern, which, in addition to the classical read and write parts from the Passthrough Replicator pattern, has a transformation layer in between.

  The transformation consists of either replacing the attributes that shouldn’t be replicated (for example, with the Anonymizer pattern) or simply removing them if they are not required for processing.

  - **Consequences**
    - Transformation risk for text file formats
      - Example: the datetime format is different from the standard used by our data processing framework. Instead of defining the timestamp columns as is, we can simply configure them as strings and not worry about any silent transformations.
    - Desynchronization
      - Data is continuously evolving, and nothing guarantees that the privacy fields we have today will still be valid in the future. Maybe new ones will appear or attributes that are not currently considered PII will be reclassified as PII.
      - To avoid these kinds of issues, if possible, we should rely on a data governance tool, such as a data catalog or a data contract in which the sensitive fields are tagged. 

  - **Example**
    - Databricks and BigQuery (or SQL): data reduction approach that eliminates unnecessary fields
    - PySpark: drop function
    - AWS Redshift: GRANT SELECT
    - Apache Spark: mapping function

## Data Compaction
  Even a perfect dataset can become a bottleneck, especially when it grows over time because of new data. As a result, at some point, metadata-related operations like listing files can take even longer than data processing transformations.
### Compactor
  The easiest way to address this issue of a growing dataset is to reduce the storage footprint of the underlying files. 

  E.g. real-time data ingestion pipeline synchronizes events from a streaming broker to an object store. The main goal is to make the data available for batch jobs within at most 10 minutes. Since it’s a simple passthrough job, the pipeline is running without any apparent issues. However, after three months, all the batch jobs are suffering from the `metadata overhead` problem due to too many small files composing the dataset. This will spend 70% of execution time on listing files to process and only the remaining 30% on processing the data. This has a serious latency and cost impact as our use pay-as-you-go services.

  Having small files is a well-known problem in the data engineering space.  Storing many small files involves longer listing operations and heavier I/O for opening and closing files. A natural solution to this issue is to store fewer files.

  Compactor pattern addresses the problem by combining multiple smaller files into bigger ones, thus reducing the overall I/O overhead on reading. Open table file formats have their dedicated compaction command that often runs a transactional distributed data processing job under the hood to merge smaller files into bigger ones as a part of the new commit.

  - **Examples**
    - Apache Iceberg: rewrite data file action
    - Delta Lake: OPTIMIZE and VACUUM command
    - Apache Hudi: merge-on-read (MoR) table
    - Apache Kafka: append-only key-based logs system

  - **Consequences**
    - Cost versus performance trade-offs
      - The compaction job is just a regular data processing job that can be compute intensive on big tables.
      - If we consider only this aspect, we should execute it rarely, such as once a day, ideally outside working hours, and outside the pipeline generating the dataset.
      - We’ll then need to choose our strategy and accept that it may not be perfect from both the cost and performance perspectives. There is no one-size-fits-all solution.
    - Consistency
      - Compaction simply rewrites already existing data. Consequently, consumers may have difficulties distinguishing the data to use from the data being compacted.
      - Compaction is much simpler and safer to implement in modern, open table file formats with ACID properties (such as Delta Lake and Apache Iceberg) than in raw file formats (such as JSON and CSV).
    - Cleaning
      - The compaction job may preserve source files. We’ll have to complete it with a cleaning job to reclaim the space taken up by the already compacted files.

## Data Readiness
  This part will answer problematic question we’ll certainly ask ourself is, “When should We start the ingestion process?”
### Readiness Marker
  The Readiness Marker is a pattern that helps trigger the ingestion process at the most appropriate moment. Its goal is to guarantee the ingestion of the complete dataset.

  E.g. In data lineage, there will be some process that need a dynamic time to execute. It will arise an issue such as: complain about incomplete datasets, and they’ve asked us to implement a mechanism that will notify them directly or indirectly—when they can start consuming our data.

  The issue is particularly visible in the logically dependent but physically isolated pipelines maintained by different teams. Because of these isolated workloads, it’s not possible for our job to directly trigger downstream pipelines. Instead, we can mark our dataset as ready for processing with the Readiness Marker pattern. 

  > The first implementation uses an event to signal the dataset’s completeness. 

  - **Example**
    - Apache Spark: flag file
    - Delta Lake: new commit log
    - the data orchestration layer: as a separate task executed after successful data processing.

  > A different implementation applies to partitioned data sources.

  If we’re generating data for time-based tables or locations, the Readiness Marker can be conventional. E.g. update hourly base partition, and get the latest update after each hour.

  - **Consequences**
    - Lack of enforcement
      - There is no easy way to enforce conventional readiness based on the flag file or the next partition detection. It’s very important to communicate with our consumers and agree upon the conditions that may trigger processing on their side. Clearly explain the risks of not respecting the readiness conventions.
    - Reliability for late data
      - If the partitions are based on the event time, the partitionbased implementation will suffer from late data issues.
      - That’s why we should either consider partitions as immutable parts that will never change once closed or clearly define and share the mutability conditions with our consumers. 

## Event Driven
  The Readiness Marker pattern from the previous section relies on pull semantics, in which the consumer is responsible for checking whether there is new data to process.

  It’s hard to predict the incoming frequency of data. Consequently, we must shift our mindset from static ingestion to event-driven ingestion.
### External Trigger
  The event-driven nature of a dataset favors push semantics, in which the producer is in charge of notifying consumers about data availability.

  With the goal of reducing costs, we want to change the scheduling mechanism and run the pipeline only when there is something new to process. The prosedure sends a notification event to a central message bus with specific topic and it will be distribute to each consumer for each topic.

  - **Three main actions**:
    - Subscribing to a notification channel.
    - Reacting to the notifications. The role of this stepis to analyze the event and decide whether:
      - It should result in triggering a pipeline in the data orchestration layer
      - Starting a job in the data processing layer.
    - Triggering the ingestion pipeline in the data orchestration or data processing layer.

  - **Consequences**
    - Push versus pull
      - The External Trigger component can implement pull or push semantics. The difference is the key in understanding the pattern’s impact on our system.
      - The pull-based trigger continuously checks whether there are new events to process, while the push-based trigger does nothing as long as the event producer doesn’t notify it about something new to process.
      - The pull-based trigger is a long-running job, so it’s a process that stays up and checks at short, regular intervals whether there is new data to process. It’s not the most optimized since the job may spend most of its time pulling zero messages from the notification source.
      - The push-based trigger, where the data source informs the endpoint(s) about new messages present in the bus. Each notification message starts a new consumer instance which finishes after reacting to the event.
    - Execution context
      - There is a risk that the external trigger may become just a ping mechanism that calls a data orchestrator endpoint.
      - It’s important to enrich the triggering call with any appropriate metadata information, including the version of the trigger job, the notification envelope, the processing time, and the event time. They will be useful in day-to-day monitoring, when we will need to investigate the reasons for any eventual failures.
    - Error management
      - The events are the key elements here, and without them, we won’t be able to trigger any work. We should design the trigger for failure with the goal in mind to keep the events whatever happens.

  - **Example**
    - Could-based event driven: AWS, Azure, and GCP provide serverless function services.
    - Data orchestrators expose an API that we can use to start a pipeline. (AWS Lambda function with Apache Airflow).

  <img src="/assets/images/data/data_pattern/data_pattern_02.webp" alt="drawing"/>


# Error Management Design Patterns
  While processing the data, we’ll face two kinds of errors. 
  - Transient errors: that are often temporary and will eventually recover automatically in the future. (a short database unavailability mitigated with automatic connection retries).
  - Nontransient errors: that are not temporary and will never recover by themselves. (unprocessable records or poison pill messages). They are fatal issues that stop the application and require our manual intervention.
## Unprocessable Records
### Dead-Letter
  An easy solution is to ignore the bad records and continue processing the correct ones. It’s easy to do if we can simply skip the invalid events and thus lose them forever. Or we can opt for another approach and save the bad records elsewhere for further investigation.

  The solution should keep the pipeline running even for the occasional failed records and give us an opportunity to investigate the errors later.

  - **Workflow**
    - Identifying places in the code where our job can fail.
    - Add some `error handling logic` / safety controls over the likely fail spots that have been identified. (try-catch block or if-else condition).
    - Add the failed message as the metadata to help us better understand the failure at the post-analysis stage.
    - Configure a `the dead-letter storage` for the erroneous events. Consider the following for destination of the erroneous events:
      - Resiliency, so that we don’t need to think about a dead-letter strategy for our dead-letter storage.
      - Monitoring ease, to better understand whether the errors are only occasional issues or whether the whole system is going down.
      - Writing performance, since writing the unprocessed records to an extra place will incur some cost in the overall job execution time.
      - Good candidates for the dead-letter stores are object stores in the cloud or streaming brokers since they’re highly available, fast, and easy to be `the monitoring layer`.
    - Add `the replay pipeline` that ingests the failed records into the main data flow.

    <img src="/assets/images/data/data_pattern/data_pattern_03.webp" alt="drawing"/>

  The difference between implementing Dead-Letter at stream processing and batch workloads comes from the data perception. 
  - Streaming operates on one record at a time and thus can write an individual record to dead-letter storage.
  - Batch works on a bunch of data, and very often, it will write a subset of the erroneous records at once to dead-letter storage.

  - **Consequences**
    - Snowball backfilling effect
      - The good thing about the fail-fast approach is its simplicity for the whole system. On the other hand, if our job doesn’t follow the fail-fast strategy, consumers will continue processing data that might be partial.
      - If we decide to run the replay pipeline, the ingested records can belong to the partitions already processed by our downstream consumers. That would require a back-filling action on their part and start a `snowball backfilling effect`, where their downstream consumers must reprocess the data as well. Mitigating this issue is not easy because each solution comes with its own trade-offs.
    - Dead-lettered records identification
      - It better to distinguish dead-lettered records from the rows added in the normal ingestion pipeline.
      - It can be useful to implement a filtering condition skipping replayed records in the downstream consumers or to simply track the origin of each row.
      - We can add a boolean column or an attribute called was_dead_lettered to indicate each record produced by the Dead-Letter replay job.
    - Ordering and consistency
      - The pattern can break data consistency. E.g. break session due to dead-letter for the range of time.
      - This is also true for the ordered data delivery requirement. In that case, any replayed failed delivery will break the ordering consistency. 
    - Error-safe functions
      - When we use error-safe functions, instead of capturing the exception, we’ll need to compare the output value with the input. If the input is present but the function returns a NULL value, it might represent a processing error and thus an unprocessable record.
      - We need to understand their error-safety semantics, which may differ from one function to another.
    - Error or failure?
      - This pattern will hide a fatal failure that should stop the pipeline.
      - We should complete the code implementation with an appropriate alerting layer that, in case of too many dropped events, could stop the job to avoid propagating potentially wrong data to our system.

  - **Examples**
    - Apache Flink: side outputs
    - Apache Kafka: try-catch block / if-else condition
    - Batch: try-catch block / if-else condition
    - Apache Spark SQL and Delta Lake: error-safe CONCAT data transformation

## Duplicated Records
  Duplication records could be happen in distributed systems, backfilling process in error management, or system behaviour.

  Exactly-once processing works only if we don’t encounter runtime errors. Otherwise, the restarted job execution may reprocess already processed records, despite the deduplication logic. This is often an accepted trade-off between automated transient errror managent and deduplication.

  > Exactly-once processing doesn’t guarantee exactly-once delivery or perfect deduplication
### Windowed Deduplicator
  The key for data deduplication is to consider the data to be limited. 
  - The streaming jobs, the limits will be `time-based windows`.
  - The batch jobs will reduce the scope to `the currently processed dataset`.

  - **Workflow**
    - Identifying the deduplication attributes that guarantee the uniqueness of each record.
    - Define the deduplication scope, to limiting compute power and slow process.
    - Execute the data

  - **Consequences**
    - Space versus time trade-off
      - This is a main consequnces of streaming pipelines, a short window will probably miss some duplicates, but on the other hand, it will have a small impact on resources.
    - Idempotent producer
      - Correctly deduplicating the data doesn’t guarantee exactly-once delivery for processed records. Very often, it will not be possible because of transient errors and their automatic solutions, such as retries. 

  - **Example**
    - Apache Spark: dropDuplicates function (for both batch and streaming jobs)
    - Batch jobs - SQL 
      - DISTINCT expression 
      - WINDOW function alongside the condition on the row_number()
    - Streaming jobs
      - Using the state store to verify whether a record has already been seen or not.
      - types of state stores. They’re all trade-offs between performance and data consistency:
        - Local: the state data lives only in memory.
        - Local with fault-tolerance: the state still primarily lives in memory and the job persists it to a remote storage for fault tolerance reasons. 
        - Remote: the state is only present in a remote data store.

    - 

## Late Data
### Late Data Detector
  The first step when dealing with data arrival issues is their detection with the Late Data Detector pattern. It can help in many situations, such as completing already processed partitions or controlling the state in stateful jobs, as we saw before for deduplication in stream processing.

  - **Workflow**
    - The pattern requires `defining one time-based attribute to track late data`. The attribute should describe when a given event happened. Otherwise, it might be impossible to classify the incoming records as being late or on time.
    - Define a latency aggregation strategy that will apply individually to each partition in our input data store. To avoid a situation in which our processing layer doesn’t move on, the latency aggregation strategy must be monotonically increasing. The most common aggregation strategy uses the `MAX function`, taking the greatest event time for each partition.
    - Decide on an additional aggregation strategy that will calculate a single event time for all partitions to represent overall progress.
      - For this global event time, we can opt to use the following:
        - The MIN function if our job needs to follow the slowest upstream dependency.
        - The MAX function that follows the fastest upstream dependency.
        - The MIN and MAX combined at different levels.

      <img src="/assets/images/data/data_pattern/data_pattern_04.webp" alt="drawing"/>

    - Add an allowed lateness attribute to allow some extra unexpected latency. The Late Data Detector pattern subtracts the allowed lateness value from the workflow’s tracked event time as `MAX(event time) - allowed lateness`. The result of this calculation is called the `watermark`, and it defines the minimum event time to consider an event as on time. 

    Example for watermark could be shown below.

    <img src="/assets/images/data/data_pattern/data_pattern_05.webp" alt="drawing"/>

  - **Consequences**
    - Prebuild Late data capture tool
    - MIN strategy, stuck-in-the-past situations, and stateful jobs
      - The partition-based event time tracker doesn’t use the MIN function in order to avoid a stuck-in-the-past situation. 
      - If we used the MIN strategy to track partition event times, it would imply the following consequences:
        - Open-close-open infinite loop
        - Stuck in the past: If our pipeline is getting late data over and over again, the watermark may never make any progress. Consequently, our eventual event time–based state will grow because we will not be able to determine the buffered items as completed with regard to the watermark.
    - Max strategy and event skew
      - In highly skewed environments, it can be too aggressive and consequently drop many records. Unfortunately, there is no silver bullet for this issue. The best mitigation strategy should rely on appropriate late events monitoring and the possibility of reintegrating late records whenever there is a high event skew.

  - **Example**
    - Apache Spark Structured Streaming: withWatermark function. A built-in capability to detect and ignore late events, but it doesn’t expose an API to capture them easily.
    - Apache Flink: provides more flexibility for both capturing and detecting late events.

### Static Late Data Integrator (Circuit Breaker / CQRS)
  By default, we can ignore late data. However, late data may also be valuable, and if it represents a significant percentage of our dataset, losing it won’t be an option.

  A fixed delay for late data ingestion is a perfect scenario where we can leverage the Static Late Data Integrator pattern.

  The easiest solution to the problem is using processing time–based partitions. However, if we do care about the event time somewhere in our system, using the processing time solution simply moves the problem somewhere else.

  E.g. processing time partition for nine o’clock has the following distribution: 80% of the data for nine o’clock, 10% for eight o’clock, and 10% for seven o’clock. One of the downstream consumers uses event time–based partitions. Hence, even though our pipeline doesn’t need to deal with late data, it generates late data that will need to be handled by other processes in the system.

  Start the implementation by defining a so-called `static lookback window` (i.e., how far to look back in the past for late data in a given job execution) with fix window duration. 

  <img src="/assets/images/data/data_pattern/data_pattern_06.webp" alt="drawing"/>

  After defining the lookback window, we need to place the late data integration process in our pipeline. 

  <img src="/assets/images/data/data_pattern/data_pattern_07.webp" alt="drawing"/>

  Some strategic that we can apply to handle this the late data integration process:
  - the sequential strategy: this is for stateful pipelines where the results generated by one execution depend on the results generated by the previous executions.
  - For stateless pipelines, we can use and switch between all three strategies. But if we want to deliver current data first, we should opt for either the second or the third approach, in which late data is handled at the same time or after the current execution time.

  > detect data that belongs to a period that has already been processed, identify the affected keys or partitions, and apply targeted corrections rather than rebuilding the entire dataset.

  - **Difference from Watermark**
    - Watermark
      - Accept data until
      - T + 10 minutes
      - After that
      - Drop it
    - Static Late Data Integrator
      - Accept forever
      - Correct historical data

  - **ELI5**
    - Imagine a teacher collects homework every day.
      - At 5 PM, she grades all homework that has arrived.
      - Some students submit late the next morning.
      - Instead of re-grading the entire class, she has a separate notebook.
    - Whenever late homework arrives:
      - Find the student's previous score.
      - Replace it with the corrected score.
      - Update the final report.
    - The homework already graded is the static dataset.
    - The late homework is the late data.
    - The notebook used to merge them is the Static Late Data Integrator.

    - The word Static refers to the fact that the primary dataset has already been finalized.
    - Rather than recomputing all data that already calculated, we integrate only this new record into the static table.
  
  - **Implementation**
    - `MERGE INTO`
    - `UPSERT`
    - `DELETE + INSERT`

  - **Use Case**
    - Original data

      | OrderID  | Revenue | 
      | -------- | ------- |
      | 1        | 100     |
      | 2        | 200     |
      | 3        | 300     |

    - Daily total: 450
    - Two days later
      ```SQL
        Late Order

        OrderID=4
        Revenue=300
        Date=Yesterday
      ```

    - Static Late Data Integrator
      ```SQL
      Find yesterday
      Current Total = 450
      450 + 300 =750
      Update yesterday only
      ```
      No need to recompute every day.
    
    - Static Late Data Intergrator (IoT)
      ```SQL
      Load 10:00-10:05 window
      Insert event
      Recalculate average
      Overwrite window
      ```

    - Static Late Data Intergrator (IoT)
      ```SQL
      Reload July 1
      Recalculate
      Publish corrected balance
      ```

  - **Architecture**

      ```sequence    
               Streaming Events
                        │
                        ▼
               Real-time Aggregation
                        │
                        ▼
              Final Daily Sales Table
                (Static Dataset)
                        │
            --------------------------
            │                        │
      Late Event Stream         Historical Table
            │                        │
            └──────────┬─────────────┘
                       ▼
            Static Late Data Integrator
                       │
                       ▼
             Corrected Historical Table
      ```
    
    The historical table is mostly immutable. Only affected records are updated.

  - **Consequences**
    - Snowball backfilling effect
      - If we are a data provider and our data consumers care about consistency, they’ll inevitably need to replay all partitions with the late data, just as we have done. If they have consumers too, those consumers will also need to run backfilling for these partitions...and in the end, the whole operation may become very compute intensive.
    - Overlapping executions and backfilling
      - we shouldn’t backfill our jobs as we would backfill jobs without the static lookback window.
    - Pipeline trigger
      - With the Static Late Data Integrator, our backfilling jobs must be part of the main pipeline. We can’t start separated pipelines as part of the lookback window–based backfilling because it’ll lead to the same problem as overlapping executions and backfilling.
      
      <img src="/assets/images/data/data_pattern/data_pattern_08.webp" alt="drawing"/>

    - Waste of resources
      - Fixed periods from the lookback window may not contain late data every time. We can add a control task to run the integration task only when there is late data.
    - Time requirement
      - If our dataset is not partitioned by time or doesn’t have any time concept, we cannot really detect and thus integrate late data. Time partitions from the Static Late Data Integrator pattern are time boundaries that each incoming record is comparing against.
    - Downstream consistency
      - Reports may already have consumed old values. Need:
        - versioning
        - CDC
        - refresh strategy

  - **Example**
    - Apache Airflow: Dynamic Task Mapping. The feature lets us create tasks dynamically from a data provider function. A perfect fit for generating late data integration tasks for the static lookback window duration.

### Dynamic Late Data Integrator
  Having a static tolerance period is not always possible, and sometimes we may need a more dynamic approach that will just load the partitions impacted by the late data.

  Using Dynamic Late Data Integrator patter to handle variability and integrate only the partitions with late data. The implementation leverages a lookback window that is dynamic, which means that all the backfilled partitions really contain late data. To make this happen, the dynamic approach requires an additional data structure to store the last execution time, and eventually, the last update time for each partition.

  <img src="/assets/images/data/data_pattern/data_pattern_09.webp" alt="drawing"/>

  <img src="/assets/images/data/data_pattern/data_pattern_10.webp" alt="drawing"/>

  - **Consequences**
    - Concurrency
      - If our pipeline supports concurrent executions, dynamic late data integration may generate duplicated late data integration runs.

      <img src="/assets/images/data/data_pattern/data_pattern_11.webp" alt="drawing"/>

      - Shows what could happen in a pipeline running four different jobs in parallel, with late data in each processed partition.
      - We need to `add an extra column` to the state table that will keep the partition status either as already processed or as being processed. -
      - Consequently, the query retrieving the partitions to backfill should add this column as an `extra filtering condition` to ignore the partitions already planned for late data integration. 
      - Each pipeline needs to `start with the task that updates the is_processed column` of the currently processed partition. That way, we can avoid having the next execution generate the current partition as the one to backfill. Also, this task should run only if the execution of the previous run succeeded.
      - The task that generates the partitions to backfill should now also `update all retrieved partitions as having been processed`. It should run only if its previous execution succeeded. This dependency on the past runs helps avoid race conditions and triggering the same partitions in two different runs.
      - `The task updating the last processed time should additionally set the Is processed flag to false`. That way, if the partition gets new late data, it can still be replayed.
      
      <img src="/assets/images/data/data_pattern/data_pattern_12.webp" alt="drawing"/>

      - If the task that generates partitions to backfill fails, its future executions will not run due to the dependency on the previous run. Consequently, the pipeline will get stuck in a long in-progress state requiring our manual intervention to unblock it.
    - Stateful pipelines and very late data
      - with the last successful run having taken place on 2024-10-20. There hasn’t been any late data so far, but the next day’s execution spots late data ingested for the partition of 2024-09-21.Since our job is stateful, we will need to regenerate all executions from 2024-09-21 to 2024-10-20 to guarantee the correctness of our dataset.
    - Scheduling complexity
      - Depending on our storage layer, getting the last modification time for each partition might not be easy. This step can involve dealing with the internal details of a storage technology or even implementing the update tracking table on our own.
  
  - **Example**
    - Apache Airflow: Dynamic Task Mapping. `depends_on_past` attribute.
    - Delta Lake: DeltaLog class

## Filter
### Filter Interceptor
 TBN

## Fault Tolerance
  A form of protection that ensures recoverability for continuous data processing workflows, such as streaming ones. The challenge with these workflows is to know when to start after stopping the job. 
### Checkpointer
  The fatal error is particularly critical in stream processing. These applications are working on continuously arriving events that are often stored in an appendonly log.

  To avoid reprocessing past data, our job must keep track of the most recent position in the consumed data source, as well as the computed state. The Checkpointer pattern implements this tracking mechanism.

  `Checkpointing` consists of recording the data processing process in a more persistens storage than the job’s environment, which may change when we restart it.

  - **Approaches**
    - Data processing framework based
      - Rely on a data processing framework, the progress information may be recorded in the environment managed by the framework itself. 
    - Data store based
      - Using the data store SDK, we may be interacting with the data store layer for the checkpoint information.

  - **Implementations**
    - Configuration driven: where we only configure the checkpointing frequency and delegate the execution to our library.
    - Intentional checkpointing action from the code. Here, after reading and processing the records, wou’ll be responsible for confirming this operation to avoid getting the same data in the next execution.

  - **Example**
    - Apache Spark Structured Streaming and Apache Flink: store the progress metadata. The `checkpointLocation` attribute.
    - Apache Kafka SDK: __consumer_offsets
    - Amazon Kinesis Client Library (KCL): checkpoint Amazon DynamoDB table.

  - **Consequences**
    - Delivery guarantee versus latency trade-off
      - Position tracking is not an expensive operation in terms of latency. It only accumulates some numbers for each input partition in memory and persists them once in a while to a persistent storage.
      - Tracking the state may have a more significant latency impact as the state will probably be many times bigger than those numeric positions.
      - we’ll need to balance the latency requirements and the processing guarantee. The more frequent the checkpoints are, the slower the job will be due to checkpoint creation overhead.
    - Exactly-once feeling
      - There could be multiple tasks working in parallel and in an asynchronous manner. If one of them fails in the middle of the work before triggering the checkpoint, the restart will involve retries and reprocessing of the already successful records.


# Idempotency Design Patterns
  Idempotency is the process that return no matter how many times we invoke the function, we always get the same result. It’s a way to ensure that no matter how many times we run a data processing job, we’ll always get consistent output without duplicates or with clearly identifiable duplicates.

  Avoiding duplicates will not always be possible. If we generate the data to a messaging system that doesn’t support transactional producers, retries can still generate duplicated entries. But this issue could be handle at consumers side that will be able to indetify those records as such.
## Overwriting
  The first idempotency family covers the data removal scenario. Removing existing data before writing new data is the easiest approach. However, running it on big datasets can be compute intensive. For that reason, to handle the removal, we can use data- or metadata-based solutions.
### Fast Metadata Cleaner
  Metadata operations are often the fastest since they don’t need to interact with the data files. We often say that the metadata part operates on the logical level instead of the physical one.  

  To achieve idempotency, the Fast Metadata Cleaner pattern relies on dataset partitioning and data orchestration. We need to define the partitioning carefully since it directly impacts the idempotency granularity.

  Granularity defines at the same time the units on top of which we can apply the metadata operations to clean the table. It has an important consequence for backfilling.

  This pattern could be used at incremental and partitioned datasets or full dataset.

  - **The adaptation consists of adding these extra steps**
    - Analyze the execution date and decide whether the pipeline should start a new idempotency granularity or continue with the previous one. 
    - Create the idempotency environment. 
    - Update the single abstraction exposing the idempotency context tables.

  <img src="/assets/images/data/data_pattern/data_pattern_13.webp" alt="drawing"/>

  - **Consequences**
    - Granularity and backfilling boundary
      - The pattern defines an idempotency granularity that is also a backfilling granularity.
      - If we replay the pipeline, we have to do it from the task that creates a partitioned table. Otherwise, we’ll end up with an inconsistent dataset.
      - if we partition the data on a weekly basis and we need to backfill for only one day, we have no choice but to rerun the whole week. This doesn’t mean we’ll have to reprocess full pipelines for other days, though. If only one day generated an invalid dataset, it’s enough to replay only the data loading step for the remaining days.
    - Metadata limits
      - Also be aware of the limits of our data store. The pattern relies on creating dedicated partitions or tables, but unfortunately, it often won’t be possible to create them indefinitely.
      - To overcome these limitation issues, we can add a freezing step to transform the mutable idempotent tables into immutable ones, thus reducing the partition scope. For example, weekly tables could turn into monthly or yearly tables if there are no possible changes after a freezing period.
    - Data exposition layer
      - The final point is about access. The dataset is not living in a single place anymore, and our end users may not want to know the internal details of the design and may instead prefer to access the data from a single point of entry.
      - Use a solution similar to a database view, such as a logical structure grouping multiple tables and exposing them as a single unit.
    - Schema evolution
      - Another challenge is schema evolution. If our idempotency tables get a new optional field, we’ll need a separate pipeline to update the schema of already existing tables.

  - **Example**
    - Scripts: Remove / secure the rows `DELETE` operation, inserts processed rows `INSERT` operation. Or better process using `TRUNCATE` or `DROP` operation.
    - Apache Airflow + PostgreSQL table: `BranchPythonOperator` + `PostgresViewManagerOperator` operator.

### Data Overwrite
  If using a metadata operation is not an option, we need to apply a data operation. When the metadata layer is unavailable or using it involves a lot of effort, we can rely on the data layer and the Data Overwrite pattern.

  Running the overwriting command doesn’t guarantee our data will disappear. If we use a data store–supporting time travel feature, thus making it possible to restore the dataset to one of its past versions, the data blocks will still be there after we execute the overwrite. They will only be deleted after the configured retention period or after running the vacuum operation to reclaim unused space if the command is supported.

  - **Solution**
    - A data processing framework
      - We may simply need to set an option while configuring our data writer. Once we’ve configured our data writer, the data processing framework will do the rest (i.e., cleaning the existing files before writing).
    - work directly with SQL
      - use a combination of `DELETE FROM` and `INSERT INTO` operations.
      - A more concise alternative to `DELETE` and `INSERT` leverages the `INSERT OVERWRITE` command. This alternative overwrites the whole table with the records from the INSERT part of the statement. `INSERT OVERWRITE` doesn’t support selecting rows to overwrite, whereas the combination of `DELETE` and `INSERT` operations does.
      - Use the data loading commands available in our data store.  such as `LOAD DATA OVERWRITE` in BigQuery, support data overwriting natively. The others should be preceded with a `TRUNCATE TABLE` command.

  - **Example**
    - Apache Spark: save mode, `.write.mode('overwrite')`.
    - Apache Flink: the write mode properties
    - Delta Lake: replaceWhere option
    - Databricks and Snowflake: `INSERT OVERWRITE` command.
    - BigQuery: `writeDisposition` in the jobs feature, `--replace=true` flag.
    - SQL: 
      - `DELETE FROM` and `INSERT INTO` operations.
      - `INSERT OVERWRITE` command.
      - `LOAD DATA OVERWRITE` in BigQuery.
      - `TRUNCATE TABLE` command.

  - **Consequences**
    - Data overhead
      - Since there is a data operation involved, the pattern can perform poorly if the overwritten dataset is big and not partitioned. We can try to mitigate this overhead by applying some storage optimizations, like partitioning. They should reduce the volume of data to overwrite and hence make the replacement action faster.
    - Vacuum need
      - A `DELETE` operation might not remove the data immediately from the disk. This happens with table file formats and relational databases, where deleted data blocks, albeit not accessible by users with `SELECT` queries, still exist on disk.
      - To reclaim the space occupied by these dead rows, we will need to run a vacuum process that will remove them for real.

## Updates
  This is the case with updated incremental datasets, in which each new version generated by our data provider contains only a subset of modified or updated data. If we try to rewrite the whole dataset, we’ll have to do some preparation work to keep only the most recent version of each entity. 
### Merger
  In a nutshell, If we don’t have the complete dataset available —for example, if we’re working with the incremental changes streamed from a database in our problem statement— we need to consider combining changes with an existing dataset. that’s what the Merger pattern does.

  The Merger pattern, requires us to interact with the data to combine new and existing rows. 

  - **Workflow**
    - Define the attributes we’re going to use to combine the new dataset with the old one. We can use a single property —such as the user ID— or combination of several properties, if it guarantees uniqueness across the dataset.
    - Find a way to combine datasets in our processing layer. The common one is the `MERGE` (aka `UPSERT`) command.
    - Define the behavior for each of the possible scenarios, which are as follows:
      - `Insert`: The entry from the new dataset doesn’t exist in our current dataset. Therefore, it’s a new record we have to add.
      - `Update`: Both datasets store a given record, but it’s very likely that the new dataset will provide an updated version of the record.
      - `Delete`: This is the trickiest case because the Merger pattern doesn’t support deletes. If a record is missing from the dataset we want to merge, nothing will happen. For that reason, deletes are only possible if they’re expressed as `soft deletes` (i.e., updates with an attribute marking a given record as removed). That way, we can detect the change and apply a hard or soft delete to our data.
    - the `MERGE` statement covering all three scenarios.

  - **Code**
    ```sql
    MERGE INTO dedp.devices_output AS target
    USING dedp.devices_input AS input
    ON target.type = input.type AND target.version = input.version
    WHEN MATCHED AND input.is_deleted = true THEN
    DELETE
    WHEN MATCHED AND input.is_deleted = false THEN
    UPDATE SET full_name = input.full_name
    WHEN NOT MATCHED AND input.is_deleted = false THEN
    INSERT (full_name, version, type) VALUES (input.full_name, input.version, input.type)
    ```

  - **Consequences**
    - Uniqueness
      -  This is the first and most important requirement. The data must define some immutable attributes we can use to safely identify each record. Otherwise, the merge logic will simply not work because instead of updating a row in case of backfilling, it might insert a new one, leading to inconsistent duplicates.
   -  I/O
      -  Merger is a data-based pattern. It works directly at the data blocks level, which makes it more compute intensive.
   -  Incremental datasets with backfilling
      -  We need to be aware of a shortcoming of the Merger pattern in the context of backfilling. In case of incremental dataset, the backfill will start from the most recent version, and leads to some of them are missing in the parts of the table at the time backfilling will occur. To mitigate this issue, we may need to implement a restore mechanism outside the pipeline that will roll back the table to the first replayed execution. It’s relatively easy to do if the database natively supports this `versioning capability`.

  - **Example**
    - Apache Airflow + SQL query: `MERGE` + `UPDATE` + `WHEN NOT MATCHED THEN` + `WHEN MATCHED THEN` +`INSERT` operation.
    - Script: `UPSERT` operation.

### Stateful Merger
  The Merger pattern lacks some consistency for datasets during the backfillings. If consistency is important, we can use stateful merger pattern.

  Whenever we need to restore a dataset, the Merger pattern won’t be enough because it focuses only on the merge action. But there is an alternative called a Stateful Merger pattern that provides data restoration capability via an extra state table.

  This extra state table involves some changes in the pipeline. The workflow now has an additional step in the beginning to restore the merged table if needed and another at the end to update the state table. 

  - **Workflow**
    - The merge operation completes, it creates a new version of the merged table.
    - The completion also triggers another task that retrieves the created table version and associates it with the pipeline’s execution time.
    - The restore process will happen only when the pipeline runs in the backfilling mode. Otherwise, it will do nothing.
    - To implement this backfilling detection logic, our data orchestrator should provide a context for the execution, and from this context, we can learn about the execution mode (backfilling or normal run), we can simply analyze this context metadata.
    - If that’s not the case, we need to implement some logic leveraging the state table. The high-level logic consists of the following:
      - Getting the version of the table created by the previous pipeline’s run. If this version is missing, it means we’ll run the pipeline for the first time or backfill the first pipeline’s execution.
      - Comparing the current dataset version with the dataset version created by the previous pipeline’s execution.
      - If the two versions are the same, there is nothing to restore as the pipeline is running in the normal mode.
      - If the two versions are different, it means the pipeline has entered into the backfilling scenario. 

  - **Consequences**
    - Versioned data stores
      - The presented implementation of the Stateful Merger pattern requires our data store to be versioned. That’s the only way we can track the state and restore the table to a prior version. If we don’t work on a database with versioning capabilities, such as table file formats, we should slightly adapt the implementation to our use case.
      - <img src="/assets/images/data/data_pattern/data_pattern_14.webp" alt="drawing"/>
      - Instead of versioning the table, the pipeline loads all raw data into a dedicated raw data table with a column storing the execution time. The backfilling detection logic verifies whether the raw data table has some records for the execution times in the future.
    - Vacuum operations
      - After the configured retention duration, they remove files that are not used anymore by the dataset. Consequently, some of the prior versions will become unavailable at that moment.
    - Metadata operations
      - Compaction doesn’t overwrite the data but only combines smaller files into bigger ones. But despite this no-data action, it also creates a new version of the table. As a result, if we always use the previous version from the state table in the restore action, we will miss the operations made between two merge runs.

  - **Example**
    - Apache Airflow: the job’s execution time + delta table version created retrieves the table version
    - Delta Lake
    - Apache Spark: `spark.sql` operation

## Database
  Rely on the databases to guarantee idempotency.
### Keyed Idempotency

