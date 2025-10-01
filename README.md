# Fraud-analysis-with-Azure-Databricks
This project showcases a fraud detection pipeline built with Azure Databricks and ADLS Gen2, structured around a Lakehouse architecture (bronze → silver → gold). Data is ingested from raw CSVs, transformed with PySpark, and enriched with business rules to compute a fraud risk score. Governance is managed with Unity Catalog, and insights are delivered through a Fraud Monitoring Dashboard in Databricks SQL.

Detailed Architecture 

This project implements a fraud detection pipeline using Azure Databricks and Azure Data Lake Storage (ADLS Gen2).
The architecture follows a multi-layer Lakehouse approach (landing → bronze → silver → gold) with governance through Unity Catalog.

-Data Ingestion: Raw CSV files are uploaded to the landing container in ADLS Gen2. They are then ingested into the bronze layer (Delta tables) using PySpark notebooks.

-Processing:
   --Silver layer applies data quality rules (valid amounts, non-null IDs, standardized fields).
   
   --Gold layer enriches transactions with business rules (e.g., high-value transactions, off-hours activity, abnormal monthly behavior) and calculates a risk_score.

-Orchestration: Databricks Jobs automate the execution of notebooks, ensuring data flows from bronze → silver → gold.

-Governance & Security: Unity Catalog manages access.
   --fraud_analyst has permission to query gold tables.
   
   --auditor has restricted access (no direct read), ensuring separation of duties.

-Monitoring & Exposure: A Fraud Monitoring Dashboard built in Databricks SQL visualizes key indicators as:
   --Daily alert volume
   
   --Top 10 customers by risk score
   
   --Percentage of suspicious transactions
   

This setup demonstrates an end-to-end Lakehouse workflow, combining data engineering, governance, and business-focused analytics for fraud detection.
