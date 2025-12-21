# End-to-End Azure Data Engineering Pipeline: Yelp Dataset

![Azure Databricks](https://img.shields.io/badge/Azure-Databricks-blue?logo=microsoftazure)
![Spark](https://img.shields.io/badge/Apache%20Spark-3.5-orange?logo=apachespark)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-Storage-lightgrey)

## 📋 Project Overview
This project demonstrates a production-grade ETL (Extract, Transform, Load) pipeline built on **Azure Databricks**. Utilizing the **Medallion Architecture**, it processes the Yelp Academic Dataset (JSON) to derive actionable insights regarding business distribution and performance across major metropolitan areas.

The pipeline ingests raw semi-structured data, cleanses and enforces schema (Silver Layer), and aggregates business metrics for analytics (Gold Layer), utilizing **Delta Lake** for ACID transactions and high-performance querying.

## 🏗️ Architecture & Tech Stack

* **Cloud Platform:** Microsoft Azure
* **Compute Engine:** Azure Databricks (Spark Core / PySpark)
* **Storage:** Azure Data Lake Storage Gen2 (ADLS)
* **Data Format:** Delta Lake (Parquet-backed with transaction logs)
* **Languages:** Python (Data Engineering), SQL (Data Analysis)


## 🚀 Pipeline Workflow (The Medallion Architecture)

### 1. 🥉 Bronze Layer (Ingestion)
* **Source:** Raw JSON data stored in Azure Data Lake Gen2.
* **Action:** Established secure connectivity using the high-performance `abfss` protocol.
* **Outcome:** Raw data ingested into a distributed Spark DataFrame.

### 2. 🥈 Silver Layer (Transformation & Cleaning)
* **Filtering:** Removed closed businesses (`is_open == 0`) to focus analysis on active market trends.
* **Schema Enforcement:** Standardized column names and data types.
* **Deduplication:** Eliminated duplicate records to ensure data quality.
* **Storage:** Persisted as a **Delta Table** (`silver_yelp_businesses`) to enable "Time Travel" and schema evolution.

### 3. 🥇 Gold Layer (Aggregation & Business Logic)
* **Analytics:** Aggregated business counts by city to identify top-performing markets.
* **Optimization:** Utilized `groupBy` and `count` transformations optimized by the Catalyst Optimizer.
* **Serving:** Registered the final output as a queryable SQL Table (`gold_city_counts`).

---

## 🔧 Technical Deep Dive: Infrastructure Upgrade
*One of the key challenges addressed during this project was infrastructure modernization.*

* **Challenge:** The initial storage solution utilized legacy Blob Storage, forcing the use of the deprecated `wasbs` protocol, which lacks hierarchical directory support.
* **Solution:** Executed an in-place upgrade of the Azure Storage Account to **Data Lake Gen2 (ADLS Gen2)**, enabling **Hierarchical Namespaces**.
* **Result:** Enabled the use of the modern `abfss` (Azure Blob File System Secure) driver, significantly improving read/write throughput and security integration.

---

## 📊 Project Visuals

### Gold Layer Analytics (Business Insight)
*Visualizing the top cities by business density, identifying Philadelphia as the primary market cluster.*

![Gold Layer Visualization](assets/business_value.png)

### SQL Verification (Data Quality)
*Verifying the engineering pipeline results using Spark SQL for ad-hoc analysis.*

![SQL Query Result](assets/sql_query_result.png)

---

## 💻 How to Run This Project

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/yourusername/azure-databricks-yelp-pipeline.git](https://github.com/yourusername/azure-databricks-yelp-pipeline.git)
    ```
2.  **Upload Notebook:** Import `Yelp_ETL_Pipeline.ipynb` into your Databricks Workspace.
3.  **Setup Storage:**
    * Create an Azure Data Lake Gen2 account.
    * Upload the `yelp_academic_dataset_business.json` file.
4.  **Configure Credentials:**
    * *Note:* The notebook has been sanitized for security. You must enter your own Storage Account Key or mount the drive using Azure Key Vault (recommended for production).
5.  **Run Pipeline:** Execute the cells sequentially to build Bronze, Silver, and Gold layers.
