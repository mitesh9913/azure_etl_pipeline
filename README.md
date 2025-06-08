# Cloud-Based ETL Pipeline Using Azure

This is my implementation of a complete end-to-end Azure data engineering solution, starting from an on-premises SQL Server database and culminating in automated Power BI reporting. The entire data pipeline—from ingestion to transformation to reporting—is built using Azure-native tools.

## 📌 Business Objective
This project was built as a hands-on learning experience to simulate real-world data engineering workflows. It focuses on cloud migration and modern ETL pipeline design, particularly beneficial for small to medium-sized businesses transitioning from local databases to the Azure ecosystem.

![pipeline](https://github.com/user-attachments/assets/06d0c0b7-a0cf-4b5e-9bf7-5060238d7d63)

## 🔧 Current Environment Setup
Used the AdventureWorks dataset from Microsoft.
Deployed a Microsoft SQL Server locally.
Loaded and managed the dataset via SQL Server Management Studio (SSMS).
Created a dedicated SQL user.
Stored credentials securely in Azure Key Vault.

### 1️⃣ Data Ingestion
Data is ingested from the local SQL Server into Azure using Azure Data Factory (ADF). Steps included:
Installing the Self-Hosted Integration Runtime (SHIR).
Creating a linked service between ADF and the local SQL Server.
Building a copy activity pipeline that moves tables into the Azure Data Lake Storage (ADLS) bronze layer.

![adf](https://github.com/user-attachments/assets/9be8be13-045d-4f0f-ac40-c76f96a39cfc)


### 2️⃣ Data Transformation
Data follows the Medallion Architecture (bronze → silver → gold).
Azure Databricks using PySpark is used to transform and optimize the data.
Raw data in Parquet format is read from the bronze layer and written to silver and gold layers in Delta Lake format.
Transformation steps:
Mount Azure Storage in Databricks.
Process and clean data from bronze to silver.
Further optimize data for analytics in the gold layer.
ADF orchestrates the execution of Databricks notebooks for seamless automation.

![2-transformation](https://github.com/user-attachments/assets/c1457373-43f4-48c0-8639-39e2ba414365)



### 3️⃣ Data Loading
Final, cleaned data in the gold layer is loaded into Azure Synapse Analytics and made accessible for reporting:
Link Azure Data Lake to Synapse.
Create SQL views using Synapse serverless SQL pool.
Register views for reporting consumption.

![synapse](https://github.com/user-attachments/assets/20792c52-49c9-439e-8e3f-02cbb654175c)

### 4️⃣ Data Reporting
Power BI connects to the Synapse SQL views using DirectQuery for live updates
Built an interactive dashboard for sales, products, and customer insights.
The dashboard dynamically reflects changes in the source database.

✅ Final Pipeline Test
To validate the pipeline end-to-end:
Two new customers were added to the local SQL database.
The pipeline successfully propagated the change through to Power BI.

![powerbi](https://github.com/user-attachments/assets/bbeddb34-79be-421f-b6d9-208b5c63d9ce)
The customer count updated from 847 to 849.
![test-pipeline](https://github.com/user-attachments/assets/135ebd48-2049-4e59-a63a-b60364d6017d)
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
