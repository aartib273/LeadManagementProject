Overview

The pipeline follows this workflow:

  Extract data from an Excel file in Azure Blob Storage.
  Load the data into an Azure SQL Staging Table (Acquisition Table).
  Transform and integrate the data into an Azure SQL Integration Table (CompanyLeads).
  Load the transformed data into Snowflake for further processing.

Data Flow: Excel → Blob Storage → Azure SQL Staging → Azure SQL Integration → Snowflake

Steps:
 - Extract: The Excel file is stored in Azure Blob Storage.
 - Load to Staging: Data is ingested into the Acquisition Table in Azure SQL.
 - Transform & Merge: The data is processed in the Integration Table to manage incremental updates.
 - Load to Snowflake: Processed data is loaded into Snowflake.
 - Event Processing (Python): A separate Python script reads data from Snowflake and processes lead events.

Implementation Details of Azure Data Factory Pipeline
 - Incremental Load: Tracks changes using UpdatedDateUtc.
 - Git Integration: Pipeline version-controlled via GitHub.
 - Failure Notifications: Sends email alerts on failures.
 - Scheduled Trigger: Runs every 30 minutes.
 - Linked Services: Connects Azure Blob Storage, SQL Database, and Snowflake.

Snowflake Integration
 - A LeadEvents table is created to track lead lifecycle events.

Python Transformation Script
