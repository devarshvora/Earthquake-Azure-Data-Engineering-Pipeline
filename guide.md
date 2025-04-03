# Comprehensive Guide: Earthquake Data Engineering Pipeline with Azure

This guide provides step-by-step instructions for setting up an automated earthquake data engineering pipeline using Azure services.

---

## Prerequisites
1. An active Azure subscription.
2. Basic knowledge of Python and Spark.
3. Familiarity with Azure services like Databricks, Data Factory, and Synapse Analytics.

---

## Step 1: Set Up Azure Resources

### 1.1 Create a Storage Account
1. Navigate to the Azure Portal → Create a new storage account.
2. Enable hierarchical namespace in advanced settings.
3. Create three containers: `bronze`, `silver`, `gold`.

### 1.2 Set Up Databricks Workspace
1. Create an Azure Databricks resource in your subscription.
2. Launch the workspace and configure a cluster with necessary libraries (`reverse_geocoder`).

### 1.3 Configure Access Permissions
1. Assign the `Storage Blob Data Contributor` role to Databricks using Managed Identity.
2. Configure external locations in Databricks for Bronze, Silver, and Gold containers.

---

## Step 2: Upload Notebooks to Databricks

### 2.1 Bronze Notebook
- Fetches raw earthquake data from the USGS API using configurable date parameters.
- Saves raw JSON files to the Bronze container.

### 2.2 Silver Notebook
- Cleanses raw data by handling missing values and converting timestamps.
- Saves structured Parquet files to the Silver container.

### 2.3 Gold Notebook
- Enriches structured data by adding country codes via reverse geocoding.
- Saves enriched Parquet files to the Gold container.

---

## Step 3: Set Up Azure Data Factory (ADF)

Azure Data Factory orchestrates the execution of notebooks for each stage of the pipeline (Bronze → Silver → Gold). The following diagram illustrates how ADF connects these stages:

![Data Factory Workflow](Data factory Workflow.jpg)

### 3.1 Create a New Pipeline
1. Add **Notebook** activities for each stage (Bronze, Silver, Gold).
2. Link each notebook activity sequentially using success dependencies (as shown in the diagram).
3. Pass parameters like start date and end date dynamically using ADF expressions.

### 3.2 Schedule Execution
Set up a trigger in ADF to execute the pipeline daily or at desired intervals.

---

## Step 4: Query Processed Data Using Synapse Analytics

### 4.1 Link Synapse Workspace to Storage Account
1. Configure external tables pointing to Gold container files.

### 4.2 Example Query
```sql
SELECT country_code, COUNT(*) AS event_count
FROM OPENROWSET(
    BULK 'https://.dfs.core.windows.net/gold/earthquake_events_gold/**',
    FORMAT = 'PARQUET'
) AS result
GROUP BY country_code;
```

---

## Step 5: Visualization (Optional)

Use Power BI to create interactive dashboards based on processed earthquake data stored in Synapse Analytics or exported CSVs.

---

## Key Considerations

### Performance Optimization:
- Replace Python UDFs with Pandas UDFs or precomputed lookup tables for scalability.

### Security:
- Store sensitive information like API keys in Azure Key Vault.
- Implement role-based access control (RBAC).

### Scalability:
- Monitor resource usage during peak loads and scale clusters as needed.

---

This guide equips you with all necessary steps to set up a robust earthquake data engineering pipeline on Azure!

Citations:
[1] ![Data Factory Workflow](Data-factory.jpg)

---

Happy coding! 🚀

