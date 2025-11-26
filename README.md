# Cosmos-DB-Azure-SQL-Migration

Cosmos DB → Azure SQL Migration using Azure Functions (Python)

This project is a one-time data migration pipeline that transfers documents from Azure Cosmos DB into Azure SQL Database using an Azure Function (HTTP Trigger, Python).

It supports:
-  Streaming data from Cosmos DB (no memory issues)
-  Batching + bulk insert into SQL
-  Flattening nested arrays (tags → ProductTags child table)
-  Retry logic for SQL transient failures
-  Final migration summary (migrated, failed, duration)

Features
- Reads all documents from Cosmos DB
- Inserts into SQL in batches
- Handles nested arrays (tags)
tags: ["apple", "phone"]
→ gets converted into rows in ProductTags table.
- Error-handling & resiliency

Migration Report

- At the end of every run, the Function returns JSON:
  - {
  "status": "Completed",
  "total_migrated": 3,
  "total_failed": 0,
  "duration_seconds": 4.76
}

Running Locally

1. Install dependencies
2. Start the Azure Function
3. Trigger migration
  - http://localhost:7071/api/MigrateCosmosToSql

Deploy to Azure :
- Login to Azure in VS Code
- Open the command palette: Ctrl + Shift + P
- Select: Azure Functions: Deploy to Function App
- Choose subscription → create new Function App → Python runtime
- Add environment variables in Azure Function Configuration
Trigger using:
- https://practice09-hnexbjbaezcba3eu.southindia-01.azurewebsites.net/api/MigrateCosmosToSql?code=Nh3TDB2pafZcX4YaIhbobEr6hS5m3xHYMFwbT8bPBCskAzFua9VObA==

Validation:

Check SQL tables:
- SELECT * FROM dbo.Products;
- SELECT * FROM dbo.ProductTags;

Check Cosmos DB:
- SELECT * FROM c

Migration Report Example :

{
  "status": "Completed",
  "total_migrated": 3,
  "total_failed": 0,
  "duration_seconds": 4.76,
  "started_at": "2025-11-26T10:56:19",
  "ended_at": "2025-11-26T10:56:24"
}




