# Olympic-pipeline-with-Azure-Devops

## Overview
This project demonstrates a fully automated data pipeline built using Azure Data Factory (ADF), Azure Databricks, and Azure Synapse Analytics, following the Medallion Architecture pattern — Bronze, Silver, and Gold layers. It leverages Azure DevOps for CI/CD and version control, and PySpark for scalable data transformations.<br>

## Project Architecture
<img width="951" height="551" alt="project architecture" src="https://github.com/user-attachments/assets/c7d801e9-747f-41db-bd0f-20d52de7c69b" />

## Bronze layer(Raw data)
* Stores raw, unprocessed data as ingested from source systems (GitHub datasets).
* Maintains data lineage and auditability by keeping the data in its original format.
* Example: .csv, .json, or .parquet files directly copied using ADF.<br>

* ### ADF Tasks:
  * Connect to GitHub raw dataset links.
  * Dynamically parameterize file names and paths.
  * Load raw data into Azure Data Lake Storage (ADLS) under the Bronze container.

* ### Azure DevOps
  * Manages source control (GitHub integration for datasets and pipeline code).
  * Automates deployment via CI/CD to Azure Data Factory and Databricks.
  * Maintains versioning for datasets and configuration files.

## Silver layer(Transformed data)
* Handles data cleansing, standardization, and schema enforcement using PySpark in Azure Databricks.
* A dynamic workflow reads data from the Bronze layer and applies transformations.

* ### Transformation Examples:
  * Removing duplicates and nulls.
  * Casting data types.
  * Standardizing date/time formats.
  * Joining reference datasets for enrichment.
 
## Gold layer(Enriched data)
* Represents business-ready curated datasets.
* Uses Delta Live Tables (DLT) for automated data quality, reliability, and monitoring.
* Data is enriched and aggregated for analytics and reporting purposes.

* ###Key Features:
  * Implemented using Databricks Delta Live Tables.
  * Ensures data freshness, quality checks, and lineage tracking.
  * Serves as a source for downstream consumption (dashboards, reports, machine learning).
 
## Warehouse - Synapse analytics
* Final storage layer for analytical workloads.
* Gold data is loaded into Azure Synapse for:
  * BI dashboards.
  * Advanced analytics and ad-hoc querying.
