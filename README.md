# Olympic-pipeline-with-Azure-Devops

## Overview
This project demonstrates a fully automated data pipeline built using Azure Data Factory (ADF), Azure Databricks, and Azure Synapse Analytics, following the Medallion Architecture pattern — Bronze, Silver, and Gold layers. It leverages Azure DevOps for CI/CD and version control, and PySpark for scalable data transformations.<br>

## Project Architecture
<img width="951" height="551" alt="project architecture" src="https://github.com/user-attachments/assets/c7d801e9-747f-41db-bd0f-20d52de7c69b" />

## Bronze layer(Raw data)
* Stores raw, unprocessed data as ingested from source systems (GitHub datasets).
* Maintains data lineage and auditability by keeping the data in its original format.
* Example: .csv, .json, or .parquet files directly copied using ADF.<br>
<img width="959" height="410" alt="Storage account after Ingestion" src="https://github.com/user-attachments/assets/bd6f003b-24f2-4e87-abfb-7945d93fb76c" /> <br>
 BRONZE LAYER AFTER INGESTION.


* ### ADF Tasks:
  * Connect to GitHub raw dataset links.
  * Dynamically parameterize file names and paths.
  * Load raw data into Azure Data Lake Storage (ADLS) under the Bronze container.<br>
<img width="959" height="407" alt="ADF final pipeline" src="https://github.com/user-attachments/assets/df78943c-cc9e-4211-be56-07c717de6fe4" /> <br>
ADF PIPELINE.

* ### Azure DevOps
  * Manages source control (GitHub integration for datasets and pipeline code).
  * Automates deployment via CI/CD to Azure Data Factory and Databricks.
  * Maintains versioning for datasets and configuration files.<br>
<img width="959" height="436" alt="Azure devops overview" src="https://github.com/user-attachments/assets/cb634362-941b-48f3-b2c8-ae29b913b4fa" />


## Silver layer(Transformed data)
* Handles data cleansing, standardization, and schema enforcement using PySpark in Azure Databricks.
* A dynamic workflow reads data from the Bronze layer and applies transformations.

* ### Transformation Examples:
  * Removing duplicates and nulls.
  * Casting data types.
  * Standardizing date/time formats.
  * Joining reference datasets for enrichment.<br>
<img width="959" height="408" alt="final silver container" src="https://github.com/user-attachments/assets/8ab1196b-1a45-4770-bab1-1258d464be30" /> <br>
FINAL SILVER CONTAINER.

 
## Gold layer(Enriched data)
* Represents business-ready curated datasets.
* Uses Delta Live Tables (DLT) for automated data quality, reliability, and monitoring.
* Data is enriched and aggregated for analytics and reporting purposes.<br>
<img width="959" height="436" alt="DLT1" src="https://github.com/user-attachments/assets/1a762f14-58c9-4517-ac2c-59c43bc8deb2" /> <br>
DLT PIPELINE.


* ### Key Features:
  * Implemented using Databricks Delta Live Tables.
  * Ensures data freshness, quality checks, and lineage tracking.
  * Serves as a source for downstream consumption (dashboards, reports, machine learning).
 
## Warehouse - Synapse analytics
* Final storage layer for analytical workloads.
* Gold data is loaded into Azure Synapse for:
  * BI dashboards.
  * Advanced analytics and ad-hoc querying.
