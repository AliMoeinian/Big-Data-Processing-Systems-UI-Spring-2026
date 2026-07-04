# Big Data Processing Systems - University of Isfahan (Spring 2026)

Welcome to the official repository for the **Big Data Processing Systems** course at the University of Isfahan, taught by **Dr. Mohammad Ali NematBakhsh**. This repository serves as a centralized hub for all the computational assignments, practical workshops, and the comprehensive capstone project delivered during the Spring 2026 semester.

## TA Team & Curriculum Design

The course materials and pipelines were engineered, structured, and coordinated by the Graduate Teaching Assistant (TA) team. As the **Lead TA**, I managed the overall curriculum architecture, Docker environments, and team coordination, while specific modules were designed by individual team members:

* **Lead TA & Coordinator:** Ali Moeinian
* **TA Team Members:** Maryam Safavi, Behnoosh Bahyani

### Module Assignment & Ownership:
* **Project 1 (Apache Kafka Theory & Practice):** Designed and delivered by Ali Moeinian.
* **Project 2 (Distributed Batch Processing with MapReduce):** Designed and delivered by Behnoosh Bahyani.
* **Project 3 (NoSQL Document Stores & Replica Sets with MongoDB):** Designed and delivered by Maryam Safavi.
* **Project 4 (Cluster Computing & SQL Analytics via Apache Spark):** Designed and delivered by Ali Moeinian.
* **Project 5 (Data Lakehouse Architecture for Enterprise Analytics):** Designed and delivered by Maryam Safavi.
* **Project 6 (Large-Scale Machine Learning Pipelines via Spark MLlib):** Designed and delivered by Behnoosh Bahyani.
* **Final Capstone Project (Real-Time Fraud Detection Lakehouse Pipeline):** Core architecture, concept, and implementation designed by Ali Moeinian, with collaborative revisions, text refinements, and feature additions by Maryam Safavi and Behnoosh Bahyani.

---

## Materials Overview

### Project 1: Distributed Streaming with Apache Kafka
* **Focus:** Core event-streaming concepts, high scalability, replication, and fault tolerance.
* **Scenario:** Students deploy a Single-Node Kafka Cluster inside Docker using KRaft or ZooKeeper mode to process synthetic user clickstream logs (`user_activity-stream`) across 4 partitions.
* **Implementation:** Includes a Python producer script streaming dynamic JSON structures (simulating actions like `page_view`, `purchase`, etc.) and an `analytics-group` Consumer Group with parallel instances writing multi-partition records into isolated outputs.

### Project 2: Large-Scale Batch Processing with MapReduce
* **Focus:** Distributed calculation paradigms using Python's `mrjob` framework.
* **Scenario:** Processing the industry-standard MovieLens dataset (comprising movies, ratings, and user-generated tags) to extract actionable entertainment patterns.
* **Implementation:** Students build individual MapReduce jobs for movie ratings profiling, automated extraction of top contextual tags per movie, tag-aware recommendation scoring, and a fully personalized user genre-matching top-5 prediction engine.

### Project 3: NoSQL Database Modeling & Replication with MongoDB
* **Focus:** Document-oriented flexible schemas, complex aggregations, and high availability systems.
* **Scenario:** Architecting a scalable data model (`MovieDB`) with interconnected collections for `Movie`, `Actor`, and `User` entities.
* **Implementation:** Writing advanced multi-stage pipelines using the MongoDB Aggregation Framework. Profiling queries using `.explain("executionStats")` to benchmark Single-field, Compound, and Text index benefits. Setting up and testing an operational 3-node MongoDB Replica Set to visually validate automated replication and Primary-to-Secondary failover recovery.

### Project 4: Distributed Computing via Apache Spark Core & SQL
* **Focus:** Master-Worker infrastructure coordination, DataFrame APIs, and low-level Resilient Distributed Datasets (RDDs).
* **Scenario:** Distributed analysis over a multi-column e-commerce dataset containing 1 million online shop sales records (`sales_data_1M.csv`).
* **Implementation:** Constructing a local cluster consisting of 1 Spark Master node and 3 Spark Worker nodes inside a unified `docker-compose.yml`. Tasks include rigorous data cleaning (handling anomalies and null entries), data manipulation through the DataFrame API and Spark SQL, and tracking partition changes (`getNumPartitions`) via low-level RDD transformations like `reduceByKey`.

### Project 5: Enterprise Data Architecture with Data Lakehouses
* **Focus:** Multi-tier reliability formatting using Medallion Architecture (Bronze, Silver, and Gold tiers).
* **Scenario:** Transforming volatile and noisy online retail transactions into high-quality data pipelines optimized for business intelligence.
* **Implementation:** Running Apache Spark over MinIO S3-compatible cloud storage, utilizing transactional open table storage formats such as Delta Lake or Apache Iceberg. Students explicitly demonstrate ACID transaction capabilities, data quality validations, custom data schema merging, and snapshot-based time travel query lookups (`VERSION AS OF`). The final outputs are connected to interactive BI frontends built using Streamlit or Apache Superset.

### Project 6: Predictive Regression Pipelines with Spark MLlib
* **Focus:** Large-scale distributed machine learning development, data sampling, and feature extraction.
* **Scenario:** Constructing an end-to-end regression model to predict the total costs of public transit trips using millions of official NYC Yellow Taxi trip records.
* **Implementation:** Handling data ingestion with Parquet columnar storage files, isolating a reproducible sample slice via random seeding, and conducting feature engineering to extract specialized datetime metrics (such as `is_rush_hour`, `is_weekend`, and `trip_duration_min`). Features are filtered via Pearson correlation analysis, vectorized using Spark ML Pipelines, and trained via Linear Regression and Gradient Boosted Trees (GBT) before checking performance metrics like RMSE, MAE, and R².

### Capstone Project: End-to-End Real-Time Fraud Detection Lakehouse Pipeline
* **Focus:** Real-time stream processing, micro-batch machine learning, and multi-component synchronization.
* **Scenario:** Creating a real-time system to ingest, process, infer, and visualize fraudulent bank card attempts from the heavily imbalanced Kaggle Credit Card Fraud dataset.
* **Implementation:** A unified big data architecture engineered entirely inside Docker Compose containing the following operational layers:
    1.  **Ingestion & Streaming:** A specialized Kafka Producer reading data slices and injecting a Wall Clock event timestamp to govern downstream operations.
    2.  **Schema Enforcement:** Integration of the Confluent Schema Registry to validate streaming payloads.
    3.  **Stream Processing:** Apache Spark Structured Streaming reading from Kafka topics, handling 10 TPS and 40 TPS workloads, applying sliding window transformations, enforcing state-store watermarks (`withWatermark`), and persisting files into MinIO bucket S3 tables via Delta Lake or Iceberg with fault-tolerant checkpoint directory configurations.
    4.  **Machine Learning Inference:** Training a Spark MLlib Random Forest classifier, mitigating heavy class imbalances, logging parameters/metrics (F1, ROC-AUC) using MLflow, and loading the model inside the streaming loop to dispatch anomalies into a separate `fraud-alerts` Kafka topic.
    5.  **Visualization Dashboard:** Real-time analytics dashboards implemented via Apache Superset or Grafana to track processing latencies and transaction distributions.

---

## License & Contact

Designed by **Ali Moeinian** as Lead Teaching Assistant for Big Data Processing Systems, University of Isfahan. For educational reuse or questions regarding implementation details, feel free to contact me via `alimoeinian.contact@gmail.com`.
