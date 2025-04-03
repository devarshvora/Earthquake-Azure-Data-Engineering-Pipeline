# Earthquake Data Engineering Pipeline with Azure

Welcome to the **Earthquake Data Engineering Pipeline** repository! This project demonstrates a scalable and automated solution for ingesting, processing, and analyzing earthquake data from the USGS Earthquake API using Azure cloud services.

## 📋 Table of Contents
- [Overview](#-overview)
- [Architecture](#-architecture)
- [Technologies and Tools](#-technologies-and-tools)
- [Medallion Architecture](#-medallion-architecture)
- [Setup Instructions](#-setup-instructions)
- [Notebooks](#notebooks)
- [Usage](#usage)
- [Contributing](#contributing)

## 🌍 Overview
This pipeline automates the ingestion of earthquake data, processes it through multiple transformation stages (Bronze, Silver, Gold layers), and makes it available for analysis. It is designed for stakeholders like:

- **Government agencies**: Emergency response planning.
- **Research institutions**: Seismic data analysis.
- **Insurance companies**: Risk assessment.

## 🏗️ Architecture
The pipeline uses Azure's modern data engineering tools to process earthquake data. Below is the workflow diagram:

![Workflow Diagram](Workflow.png)

### Key Components:
- **Azure Data Factory**: Orchestrates the pipeline and triggers notebooks.
- **Azure Databricks**: Processes data in Bronze, Silver, and Gold layers.
- **Azure Data Lake Storage Gen2**: Stores raw, cleaned, and enriched datasets.
- **Azure Synapse Analytics**: Enables querying and analytics on processed data.
- **Power BI (Optional)**: Creates interactive dashboards for visualization.

## 🛠️ Technologies and Tools
- Azure Data Factory
- Azure Databricks
- Azure Data Lake Storage Gen2
- Azure Synapse Analytics
- Python (with libraries like `reverse_geocoder`)
- Power BI (Optional)
- Azure Active Directory & Key Vaults (for security)

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

## 🚀 Setup Instructions
1. **Create an Azure account** and set up resources:
   - Azure Data Lake Storage (Bronze, Silver, Gold containers).
   - Azure Databricks workspace.
   - Azure Synapse Analytics workspace.
2. **Clone this repository** and upload the notebooks (Bronze, Silver, Gold) to Databricks.

## 📒 Notebooks
- `bronze_layer.ipynb`: Ingests raw earthquake data from USGS.
- `silver_layer.ipynb`: Cleans and normalizes the data.
- `gold_layer.ipynb`: Enriches the data for analytics.

## 📌 Usage
1. Run the **Azure Data Factory pipeline** to trigger the process.
2. Use **Databricks notebooks** to transform data in stages.
3. Query processed data using **Azure Synapse Analytics**.
4. (Optional) Build visualizations in **Power BI**.

## 🤝 Contributing
Contributions are welcome! Please fork this repository and submit a pull request with improvements.


