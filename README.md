# Earthquake Data Engineering Pipeline with Azure

Welcome to the Earthquake Data Engineering Pipeline repository! This project demonstrates an end-to-end data engineering solution for ingesting, processing, and analyzing earthquake data from the USGS Earthquake API using Azure Cloud Services. The pipeline is designed to provide clean, enriched, and ready-to-use datasets for analytics and visualization.

## 📋 Table of Contents
- [Overview](#-overview)
- [Architecture](#-architecture)
- [Technologies and Tools](#-technologies-and-tools)
- [Medallion Architecture](#-medallion-architecture)
- [Setup Guide](#-setup-guide)
- [Notebooks](#-notebooks)
- [Usage](#-usage)
- [Contributing](#-contributing)

## 🌍 Overview
The Earthquake Data Engineering Pipeline automates the ingestion of earthquake data from the USGS API, processes it through multiple transformation stages, and makes it available for analysis. This pipeline is ideal for stakeholders such as:

- **Government agencies**: Emergency response planning.
- **Research institutions**: Seismic event analysis.
- **Insurance companies**: Risk assessment.

## 🏗️ Architecture
The pipeline follows a modular architecture leveraging Azure's cloud services. Here's an overview of the workflow:

![Workflow Diagram](https://pplx-res.cloudinary.com/image/upload/v1743654969/user_uploads/qaDihEmqUulWyGY/Workflow.jpg)

### Components:
- **Azure Data Factory**: Orchestrates the pipeline and triggers notebooks.
- **Azure Databricks**: Processes data in Bronze, Silver, and Gold layers.
- **Azure Data Lake Storage Gen2**: Stores raw, cleaned, and enriched datasets.
- **Azure Synapse Analytics**: Enables querying and analytics on processed data.
- **Power BI (Optional)**: Creates interactive dashboards for data visualization.

## 🛠️ Technologies and Tools
- Azure Data Factory
- Azure Databricks
- Azure Data Lake Storage Gen2
- Azure Synapse Analytics
- Python (with libraries like reverse_geocoder)
- Power BI (Optional)
- Azure Active Directory & Key Vaults (for security and governance)

## 🗂️ Medallion Architecture
The pipeline implements a **medallion architecture** to process data in stages:

### **Bronze Layer**:
- Raw earthquake data ingested from the USGS API.
- Stored in JSON format for reprocessing if needed.

### **Silver Layer**:
- Cleaned and normalized data.
- Handles duplicates, missing values, and converts timestamps.

### **Gold Layer**:
- Enriched data with additional context (e.g., country codes).
- Optimized for analytics and reporting.

## 🚀 Setup Guide
1. Create an Azure account.
2. Set up Azure resources:
   - Azure Data Lake Storage (Bronze, Silver, Gold containers).
   - Azure Databricks workspace.
   - Azure Synapse Analytics workspace.
3. Clone this repository and upload the notebooks (Bronze, Silver, Gold) to Databricks.
4. Configure Azure Data Factory to orchestrate the pipeline.
5. For detailed setup instructions, refer to the Guide.

## 📓 Notebooks
This repository includes three key notebooks:

- **Bronze Notebook**: Ingests raw earthquake data from the USGS API.
- **Silver Notebook**: Cleanses and structures the raw data into a tabular format.
- **Gold Notebook**: Enriches the structured data with geographical context.

## 📊 Usage
### Running the Pipeline
- Trigger the pipeline via Azure Data Factory or schedule it for daily execution.
- Query processed data using Azure Synapse Analytics or visualize it in Power BI.

### Example Query
```sql
SELECT country_code, COUNT(*) AS earthquake_count
FROM OPENROWSET(
    BULK 'https://<storage_account>.dfs.core.windows.net/gold/earthquake_events_gold/**',
    FORMAT = 'PARQUET'
) AS result
GROUP BY country_code;
```

## 🤝 Contributing
Contributions are welcome! Feel free to fork this repository, make changes, and submit a pull request.
