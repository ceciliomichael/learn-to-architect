# Data Engineering Learning Path

This path is for a complete beginner who wants to build reliable systems that collect, organize, transform, and deliver data. A data engineer does more than move files. The job includes understanding what data means, protecting its quality, recovering failed work, controlling cost, and making results trustworthy for other people and systems.

## What is available now

The repository already contains the three shared courses that begin this path:

- [Git](../learn-to-git/README.md) teaches safe project history, collaboration, automation, and recovery.
- [SQL](../learn-to-sql/README.md) teaches relational data, joins, transactions, schemas, indexes, window functions, PostgreSQL, security, and query tuning.
- [Python](../learn-to-python/README.md) teaches programming, files, JSON, CSV, packages, testing, databases, concurrency, asynchronous work, logging, configuration, profiling, and secure project boundaries.
- [Data Engineering](../learn-to-data-engineer/README.md) applies those foundations through 42 ordered modules covering the complete path below.

Complete the shared courses in the beginner order, then enter the Data Engineering course. Later focus areas remain choices rather than hidden prerequisites.

## Beginner order

Follow this order if you have no programming experience:

1. Complete Git Modules 01 through 13. This is enough Git to keep exercises safe and work with a remote repository.
2. Complete Python Modules 01 through 32. These modules teach programming and the standard data types needed by later pipeline work.
3. Complete the entire SQL course. SQL is a central data engineering language, not an optional database extra.
4. Complete Python Modules 33 through 38. These modules now build on your SQL knowledge and introduce production-oriented Python.
5. Return to Git Modules 14 through 29 while building the larger projects in this path. Recovery, investigation, hooks, tags, and long-lived repository maintenance make more sense once your projects have history.

Do not rush into Spark, Kafka, or a cloud platform before this foundation. Those tools distribute work, but they do not remove the need to understand files, schemas, SQL, failure, and testing.

## Data Engineering course sequence

The stages below are implemented in [Learn Data Engineering](../learn-to-data-engineer/README.md).

### Stage 1: Data Systems Foundations

Learn the terminal, environment variables, processes, permissions, networking basics, HTTP, containers, scheduled work, and the difference between local disks, databases, and object storage.

You should be able to run a service locally, inspect its logs, pass configuration without hardcoding secrets, and explain where its data survives after the process stops.

### Stage 2: Data Files, Schemas, and Contracts

Learn CSV, JSON, newline-delimited JSON, compression, Parquet, columnar storage, partitions, schema inference, explicit schemas, schema evolution, timestamps, time zones, decimals, null values, and data contracts.

You should be able to reject malformed input, preserve raw source data, write a documented clean dataset, and explain why changing a column can break a consumer.

### Stage 3: Warehouses and Data Modeling

Move from application-oriented normalized tables into analytical modeling. Learn facts, dimensions, grain, surrogate keys, slowly changing dimensions, snapshots, incremental models, semantic meaning, and warehouse performance.

You should be able to state the grain of every table and prevent totals from changing because of an incorrect join.

### Stage 4: Ingestion, Transformation, and Analytics Engineering

Build extract, load, and transform flows using Python and SQL. Learn idempotency, checkpoints, watermarks, incremental loads, change data capture concepts, reconciliation, backfills, late data, retries, and tests around transformations. Introduce dbt only after the SQL and modeling rules are understood.

You should be able to rerun a date range without duplicating records and prove that source totals reconcile with destination totals.

### Stage 5: Workflow Orchestration

Learn workflows, tasks, dependencies, schedules, data intervals, retries, timeouts, concurrency limits, backfills, alerts, secrets, and deployment. Use Apache Airflow as the concrete implementation after first building a small scheduler-independent pipeline.

The orchestrator should coordinate work. It should not hide all transformation logic inside one large workflow file.

### Stage 6: Distributed Batch Processing

Learn why one machine stops being enough, then study partitions, shuffles, joins, skew, serialization, lazy execution, query plans, caching, memory, and fault recovery. Use Spark DataFrames and Spark SQL before lower-level distributed APIs.

You should be able to explain why a distributed job is slow from evidence in its plan and runtime metrics, not from guesswork.

### Stage 7: Event and Streaming Data

Learn producers, consumers, topics, partitions, offsets, consumer groups, ordering, replay, delivery guarantees, idempotent sinks, event time, processing time, windows, watermarks, and late events. Use Kafka for durable event transport and Structured Streaming for one processing implementation.

Streaming is not simply a batch job running every second. State, time, replay, and out-of-order events need their own lessons.

### Stage 8: Quality, Observability, Lineage, and Governance

Apply quality checks at every earlier stage, then study them as a complete operating system. Cover freshness, volume, schema, distribution, reconciliation, service-level objectives, lineage, ownership, catalogs, access control, retention, deletion, sensitive data, incident response, and audit evidence.

Monitoring a process is not enough. A successful process can still publish incorrect or stale data.

### Stage 9: Cloud and Data Platform Operations

Deploy the same concepts using one cloud provider. Learn infrastructure as code, identity and access management, secret storage, object storage, managed databases, compute choices, queues, networking, continuous delivery, environment promotion, disaster recovery, and cost controls.

Learn one provider deeply after understanding the portable concepts. Do not memorize three clouds at once.

## Choose a later focus

After the shared sequence, choose the work that matches your goals:

- **Analytics engineering:** Deeper SQL modeling, semantic layers, metrics, governance, and self-service analytics.
- **Batch data platforms:** Large backfills, distributed computation, lakehouse tables, and platform reliability.
- **Real-time data:** Event contracts, stream processing, low-latency serving, and replay operations.
- **Machine-learning data platforms:** Feature pipelines, training datasets, online and offline consistency, and model-data lineage.
- **Data platform engineering:** Reusable internal tools, tenancy, policy, cost allocation, and developer experience.

These are branches, not five required tool collections.

## Project milestones

Progress should be demonstrated through several projects instead of one final assessment:

1. Build a local Python and SQL pipeline that reads versioned raw files, validates records, loads a database, and produces a tested analytical table.
2. Make the pipeline incremental and rerunnable, then perform a backfill and reconcile its output.
3. Orchestrate the same pipeline with retries, timeouts, alerts, logs, and an intentionally failed run that you recover.
4. Process a larger partitioned dataset with Spark and explain its execution plan.
5. Build a small event pipeline with replay, duplicate handling, late events, and an idempotent destination.
6. Deploy one project with least-privilege access, monitored freshness, lineage, cost limits, and a rollback procedure.

There is no miscellaneous stage and no final assessment.

## Accuracy anchors for future modules

Future course modules should be checked against current primary documentation:

- [Apache Airflow core concepts](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/index.html)
- [Apache Spark SQL and DataFrames](https://spark.apache.org/docs/latest/sql-programming-guide.html)
- [Apache Spark Structured Streaming](https://spark.apache.org/docs/latest/streaming/index.html)
- [Apache Kafka documentation](https://kafka.apache.org/documentation/)
- [dbt Developer Hub](https://docs.getdbt.com/)
- [OpenLineage](https://openlineage.io/)
