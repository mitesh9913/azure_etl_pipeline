# Cloud-Based ETL Pipeline Using Azure

This is my implementation of a complete end-to-end Azure data engineering solution, starting from an on-premises SQL Server database and culminating in automated Power BI reporting. The entire data pipeline—from ingestion to transformation to reporting—is built using Azure-native tools.

## 📌 Business Objective
This project was built as a hands-on learning experience to simulate real-world data engineering workflows. It focuses on cloud migration and modern ETL pipeline design, particularly beneficial for small to medium-sized businesses transitioning from local databases to the Azure ecosystem.



## 🔧 Current Environment Setup
Used the AdventureWorks dataset from Microsoft.
Deployed a Microsoft SQL Server locally.
Loaded and managed the dataset via SQL Server Management Studio (SSMS).
Created a dedicated SQL user named mrk.
Stored mrk's credentials securely in Azure Key Vault.

### 1️⃣ Data Ingestion
Data is ingested from the local SQL Server into Azure using Azure Data Factory (ADF). Steps included:
Installing the Self-Hosted Integration Runtime (SHIR).
Creating a linked service between ADF and the local SQL Server.
Building a copy activity pipeline that moves tables into the Azure Data Lake Storage (ADLS) bronze layer.



### 2️⃣ Data Transformation
Data follows the Medallion Architecture (bronze → silver → gold).
Azure Databricks using PySpark is used to transform and optimize the data.
Raw data in Parquet format is read from the bronze layer and written to silver and gold layers in Delta Lake format.
Transformation steps:
Mount Azure Storage in Databricks.
Process and clean data from bronze to silver.
Further optimize data for analytics in the gold layer.


ADF orchestrates the execution of Databricks notebooks for seamless automation.



### 3️⃣ Data Loading
Final, cleaned data in the gold layer is loaded into Azure Synapse Analytics and made accessible for reporting:
Link Azure Data Lake to Synapse.
Create SQL views using Synapse serverless SQL pool.
Register views for reporting consumption.

### 4️⃣ Data Reporting
Power BI connects to the Synapse SQL views using DirectQuery for live updates
Built an interactive dashboard for sales, products, and customer insights.
The dashboard dynamically reflects changes in the source database.

✅ Final Pipeline Test
To validate the pipeline end-to-end:
Two new customers were added to the local SQL database.
The pipeline successfully propagated the change through to Power BI.
The customer count updated from 847 to 849.


🎉 Test passed: Real-time updates confirmed!

## 🧠 Conclusion and Learnings
This project illustrates the implementation of a scalable, modular ETL system using modern Azure technologies. Some considerations:
Dataset size was intentionally small (~7MB) to minimize costs.
ADF alone could have handled the project, but other tools (Databricks, Synapse) were included to emulate a more realistic enterprise architecture.

This project helped me gain hands-on experience with:
Azure Data Factory
Azure Key Vault
Databricks and Delta Lake
Azure Synapse Analytics
Power BI integrations
