# Azure Data Factory Incremental Data Ingestion Pipeline

## 📌 Project Overview

This project implements a scalable and reusable **Azure Data Factory (ADF)** pipeline to ingest data incrementally from **Azure SQL Database** into **Azure Data Lake Storage Gen2** in **Parquet** format. The pipeline follows industry-standard incremental loading practices using a CDC-based timestamp mechanism, supports historical backfilling, and includes automated failure notifications.

The solution is designed to be **dynamic, configurable, and reusable**, requiring minimal code changes to onboard new source tables. Version control and collaboration are managed using **Git integration**.

---

## 🏗️ Architecture Overview

**Source**: Azure SQL Database
**Orchestration**: Azure Data Factory
**Storage**: Azure Data Lake Storage Gen2
**File Format**: Parquet
**Metadata Store**: JSON file (last processed timestamp)
**Version Control**: Git

---

## ⚙️ Key Features

* Incremental data ingestion using CDC timestamp column
* JSON-based watermarking to track last successful load
* Backfilling support for historical data loads
* Parquet-based storage for optimized analytics
* Automated failure notification using Web Activity
* Empty file detection and cleanup when no new data is available
* Dynamic and reusable pipeline design
* Git-based collaboration and version control

---

## 🔄 Pipeline Workflow

1. Read configuration and source table metadata
2. Retrieve the last processed timestamp from a JSON file
3. Extract only new or updated records from Azure SQL Database
4. Load data into ADLS Gen2 in Parquet format
5. Validate output file for record count
6. If no new data is present, trigger a delete activity to remove the generated empty file
7. Update the JSON file with the latest processed timestamp (when applicable)
8. Trigger Web Activity to send email alerts on pipeline failure

---

## 📂 Incremental Load Strategy

* Uses a **CDC / updated_at timestamp column** from source tables
* Maintains a **JSON watermark file** to persist the last processed timestamp
* Ensures idempotent and reliable incremental processing
* Supports backfilling by resetting or parameterizing watermark values

---

## 🔁 Backfilling Capability

The pipeline supports historical data loads by:

* Allowing configurable start timestamps
* Reprocessing past data ranges when required
* Using the same pipeline logic without code duplication

---

## 🚨 Failure Handling & Notifications

* Pipeline failures are captured at the final stage
* A **Web Activity** triggers an automated email notification
* Alerts notify users to investigate and fix pipeline issues
* Ensures improved monitoring and faster issue resolution

---

## 🧹 Empty File Handling

* When the source SQL Database contains no new or updated records, the pipeline still generate an output file with no data
* The pipeline validates the record count after ingestion
* If an empty file is detected, a dedicated **Delete activity** is triggered
* Prevents unnecessary storage usage and keeps the data lake clean

---


## 🔀 Version Control & Collaboration

* Integrated with **Git** for source control
* Enables collaborative development and change tracking
* Supports CI/CD best practices

---

## 🛠️ Technologies Used

* Azure Data Factory
* Azure SQL Database
* Azure Data Lake Storage Gen2
* Parquet
* JSON
* Git

---


## 👤 Author

Janith Shihara

---
