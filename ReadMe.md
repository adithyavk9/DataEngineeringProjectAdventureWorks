# Azure Data Engineering Project

This project is a comprehensive data engineering solution that leverages Microsoft Azure to process, analyze, and visualize data from the Adventure Works dataset available on Kaggle. It showcases how Azure services like Data Factory, Data Lake, Databricks, and Synapse Analytics can be used to build scalable, end-to-end data pipelines. From raw data ingestion (Bronze Layer) to analytics-ready transformation (Gold Layer), this project provides practical insights into designing real-world data workflows.

## Project Overview

The project follows the Medallion Architecture and is divided into three phases to systematically build the data engineering solution:

### Phase 1: Bronze Layer - Raw Data Ingestion
This layer acts as a landing zone for raw data. It follows the table structure of the source itself. In this phase:
- Dataset files are loaded into GitHub.
- Azure Data Factory (ADF) pipelines are used to pull data from GitHub.
- The data is then loaded into Azure Data Lake Storage Gen2 (ADLS Gen2).

1. **Create a Resource Group**
   - A Resource Group is a logical container that holds all related resources, allowing them to be managed as a single entity.
   - Create a new Azure Resource Group named 'AWPROJECT' to organize all resources for this project.

2. **Create a Storage Account (ADLS Gen 2)**
   - Azure Data Lake Storage Gen 2 is a cloud storage solution accessible from anywhere in the world over HTTP or HTTPS via REST API, supporting a hierarchical namespace.
   - Configure an Azure Data Lake Storage Gen 2 account named 'mydatalakeavk8089' inside the 'AWPROJECT' Resource Group for storing raw, intermediate, and processed data.
   - Enable the hierarchical namespace option.
   - Create three containers inside ADLS:
     - **bronze**: For storing raw data.
     - **silver**: For storing cleaned and processed data.
     - **gold**: For storing analytics-ready data.

3. **Set Up Azure Data Factory**
   - Azure Data Factory (ADF) is a cloud-based data integration service that allows you to create, schedule, and orchestrate data workflows across various data sources.
   - Create an Azure Data Factory instance named 'adf-aw-project-avk' inside the 'AWPROJECT' Resource Group.
   - Launch the Azure Data Factory Studio to start designing the pipeline.
   - Create a new pipeline and drag and drop a **Copy Activity** to copy data from the source (GitHub) to the destination (ADLS Gen2).
   - Add a **For Each Activity** to iterate dynamically over the dataset entities, making the data loading process scalable and efficient.
   - Configure the pipeline to handle multiple datasets and load them into the **bronze** container as part of the Bronze Layer.

### Phase 2: Silver Layer - Data Transformation
Azure Databricks is an Apache Spark-based analytics platform optimized for the Microsoft Azure cloud. It enables scalable data engineering, machine learning, and big data processing.

In this phase:
- **Clean and process raw data stored in the Bronze Layer** to create structured and enriched datasets using Azure Databricks.
- Steps to implement:
  1. **Create an Azure Databricks Workspace**: Set up an Azure Databricks instance within the 'AWPROJECT' Resource Group.
  2. **Access ADLS with Azure Key Vault**: Create an application in Azure Active Directory and store its credentials in Azure Key Vault. Assign the necessary roles to allow Databricks to access ADLS Gen2.
  3. **Go to the Workspace and Create a Notebook**:
     - Develop a notebook to load raw data from the Bronze Layer.
     - Use PySpark functions and methods for data cleaning and transformation.
  4. **Transform Data**:
     - Load data from the Bronze container.
     - Apply transformations (e.g., filtering, deduplication, data type casting).
     - Save the processed data to the Silver container in ADLS Gen2.

This step ensures the data in the Silver Layer is structured, consistent, and ready for further enrichment or analytics.

### Phase 3: Gold Layer - Analytics-Ready Data
Azure Synapse Analytics is a limitless analytics service that brings together data integration, enterprise data warehousing, and big data analytics.

In this phase:
- **Set up Azure Synapse Workspace**: Create a new Synapse workspace within the 'AWPROJECT' Resource Group.
- **Create a Dedicated SQL Pool (Data Warehouse)**: Set up a dedicated SQL pool for high-performance data querying and storage.
- **Create a Database**: Within the SQL pool, create a database to organize the analytics-ready data.
- **Ingest Data Using OPENROWSET**: Use the OPENROWSET function to load data from the Silver container into the Synapse database for analysis.
- **Schema Creation**: Define schemas and tables for structured storage of data.
- **Create Views and External Tables**: Develop views and external tables to simplify data querying and enable seamless integration with other tools.
- **Connect Synapse to Power BI**: Set up the SQL endpoint in Synapse to connect to Power BI for visualization and reporting.

This phase ensures that the data is optimized for business intelligence and advanced analytics, providing actionable insights through seamless integration with Power BI.


## Getting Started
1. Clone this repository to your local environment.
2. Follow the steps in Phase 1 to set up the required Azure resources.
3. Use the provided configuration files and templates for quick deployment.

Stay tuned for detailed instructions on subsequent phases!

