# End_To_End_ETL_Pipeline_With_Microsoft_Azure

## **Project Overview:**
Designed and implemented a scalable ETL pipeline on Microsoft Azure, following the Medallion Architecture (Bronze, Silver, Gold layers) to enable efficient data ingestion, transformation, and reporting for web-based datasets. The pipeline leveraged a combination of Azure services including Azure Data Factory (ADF), Azure Data Lake Storage (ADLS), Azure Databricks, Azure Synapse Analytics, and Power BI.

## **Architecture Diagram** :

![Architecture](https://github.com/user-attachments/assets/4856b374-3df9-433c-93c0-bed26efd781f)


## **Implementation:**

🔶 **Bronze Layer – Raw Data Ingestion:**

**Source:** Web-based HTTP data.

**Process:**
1. Developed a dynamic ADF pipeline to ingest raw data from web sources using HTTP as the source.
2. Created linked services and datasets for both source (HTTP) and sink (Azure Data Lake Storage - ADLS).
3. Parameterized the pipeline to dynamically ingest data from varying relative URLs, and to route output into configurable folders and filenames in the Bronze container.
4. Stored the raw data in CSV format in the Bronze container of ADLS.

**⚙️ Silver Layer – Data Transformation:**

**Security & Access:**
1. Configured application-level access to ADLS using Azure Key Vault for secure secret management.
2. Established connection to Databricks with Key Vault-backed secrets.

**Process:**

1. Created a Databricks cluster for distributed data processing.
2. Used Pyspark scripts to clean and transform raw CSV data from the Bronze layer.
3. Converted cleaned data into optimized Parquet format and stored it in the Silver container of ADLS for efficient downstream querying.

**🪙 Gold Layer – Data Modeling & Serving:**

**Security & Access:**
1. Utilized Managed Identity for secure access to the Silver layer in ADLS.

**Process:**
1. Queried Silver-layer parquet files using the OPENROWSET() function.
2. Created external data sources, file formats, and external tables to logically structure the data.
3. Built SQL views over the transformed data to serve as a semantic layer.
4. Wrote the final curated datasets into the Gold container in ADLS, stored in Parquet format for BI consumption.

**📊 Business Intelligence Layer:**

**Integration:**
1. Connected Power BI to the Azure Synapse Serverless SQL Pool using the Serverless SQL endpoint.
2. Developed interactive dashboards and visualizations to derive insights from the Gold-layer data.

## **Key Technologies Used:**


1. Compute & Orchestration: [![Azure Data Factory](https://img.shields.io/badge/Azure%20Data%20Factory-0072C6?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/en-us/products/data-factory) [![Azure Databricks](https://img.shields.io/badge/Azure%20Databricks-FF4F00?style=for-the-badge&logo=databricks&logoColor=white)](https://www.databricks.com/) [![PySpark](https://img.shields.io/badge/PySpark-FF9900?style=for-the-badge&logo=apachespark&logoColor=white)](https://spark.apache.org/docs/latest/api/python/)

2. Storage: [![Azure Data Lake Storage Gen2](https://img.shields.io/badge/Azure%20Data%20Lake%20Storage%20Gen2-0072C6?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) – Bronze, Silver, Gold containers

3. Security: [![Azure Key Vault](https://img.shields.io/badge/Azure%20Key%20Vault-68217A?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/en-us/products/key-vault)
[![Managed Identity](https://img.shields.io/badge/Managed%20Identity-008272?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview)

4. Data Warehouse: [![Azure Synapse Analytics](https://img.shields.io/badge/Azure%20Synapse%20Analytics-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/en-us/products/synapse-analytics) (Serverless SQL Pool)

5. Visualization: [![Power BI](https://img.shields.io/badge/PowerBI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)

6. Functional Skills: [![ETL](https://img.shields.io/badge/ETL-grey?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgaGVpZ2h0PSIxNiI+PHJlY3Qgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2IiBmaWxsPSIjZ2V5IiByeD0iMyIvPjxwYXRoIGZpbGw9IndoaXRlIiBkPSJNMTEgOEw1IDEybTYtNEw1IDQiIHN0cm9rZT0id2hpdGUiIHN0cm9rZS13aWR0aD0iMiIvPjwvc3ZnPg==)](#)
