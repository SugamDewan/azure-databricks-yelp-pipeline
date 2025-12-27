# End-to-End Azure Data Engineering Pipeline: Yelp Dataset

![Azure Databricks](https://img.shields.io/badge/Azure-Databricks-blue?logo=microsoftazure)
![Spark](https://img.shields.io/badge/Apache%20Spark-3.5-orange?logo=apachespark)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-Storage-lightgrey)

End-to-End Azure Data Engineering: Sanitized Client Case Study
📋 Project Context & Scope
This repository contains a sanitized Proof of Concept (POC) derived from a production-scale Data Lakehouse solution designed for a client in the retail and hospitality sector.

Note on Data Privacy: Due to non-disclosure agreements (NDAs), proprietary business logic and private datasets have been removed. This demonstration utilizes the Yelp Academic Dataset as a structural proxy to showcase the underlying architecture, data quality frameworks, and infrastructure optimizations delivered to the client.

🏗️ Architecture & Tech Stack
Cloud Platform: Microsoft Azure

Compute Engine: Azure Databricks (Spark Core / PySpark)

Storage: Azure Data Lake Storage Gen2 (ADLS)

Data Format: Delta Lake (Parquet-backed with transaction logs)

Languages: Python (Data Engineering), SQL (Data Analysis)

🚀 Pipeline Workflow (The Medallion Architecture)
1. 🥉 Bronze Layer (Ingestion)
Source: Raw semi-structured JSON data.

Action: Established secure connectivity to ADLS Gen2 using the high-performance abfss protocol.

Outcome: Raw data successfully ingested into a distributed Spark DataFrame, preserving the source of truth.

2. 🥈 Silver Layer (Transformation & Cleaning)
Filtering: Removed inactive business records to ensure analytical relevance.

Schema Enforcement: Implemented strict schema definitions and standardized naming conventions.

Deduplication: Applied logic to eliminate redundant records, ensuring data integrity.

Storage: Persisted as a Delta Table to enable ACID transactions and "Time Travel" capabilities.

3. 🥇 Gold Layer (Aggregation & Business Logic)
Analytics: Developed high-level aggregates to calculate business density and market distribution by city.

Optimization: Leveraged Spark's Catalyst Optimizer for efficient groupBy and aggregation tasks.

Serving: Registered the final output as a queryable SQL Table for downstream BI consumption.

🔧 Technical Deep Dive: Infrastructure Modernization
A key requirement for this client was modernizing their legacy storage architecture to improve throughput and security.

Legacy Challenge: The initial environment utilized standard Blob Storage and the deprecated wasbs protocol, which lacks hierarchical directory support and is suboptimal for large-scale Spark workloads.

The Solution: Executed an in-place upgrade to Data Lake Gen2 (ADLS Gen2), enabling Hierarchical Namespaces.

The Result: Enabled the modern abfss driver, significantly improving file-level security and read/write performance for the Spark engine.

📊 Project Visuals
Market Density Analysis (Gold Layer)
Identifying primary market clusters for the client. Based on the proxy data, Philadelphia emerged as the hub with the highest density.
(gold_layer_viz.png)

SQL Validation (Data Quality)
Verifying pipeline outputs using Spark SQL to ensure data readiness for business analysts.
(sql_verification.png)

💻 Deployment & Usage
Clone: git clone https://github.com/SugamDewan/azure-databricks-yelp-pipeline.git

Import: Upload the .ipynb notebook to your Databricks workspace.

Set up Storage: Configure an ADLS Gen2 account and upload the source JSON.

Authentication: Update the sanitized credentials section with your specific storage keys (or use Azure Key Vault).

👤 Author
Sugam Dewan Data Engineer | Cloud Specialist View My Portfolio | Connect on LinkedIn
    * Upload the `yelp_academic_dataset_business.json` file.
4.  **Configure Credentials:**
    * *Note:* The notebook has been sanitized for security. You must enter your own Storage Account Key or mount the drive using Azure Key Vault (recommended for production).
5.  **Run Pipeline:** Execute the cells sequentially to build Bronze, Silver, and Gold layers.
