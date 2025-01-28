Jan 27 2025 at 14:54
_Tags:_ #database #azure #synapse 
## Create external database objects
---
>You can use the OPENROWSET function in SQL queries that run in the default **master** database of the built-in serverless SQL pool to explore data in the data lake.

However, sometimes you may want to create a custom database that contains some objects that make it easier to work with external data in the data lake that you need to query frequently.

#### Creating a Database

You can create a database in a serverless SQL pool just as you would in a SQL Server instance. You can use the graphical interface in Synapse Studio, or a **CREATE DATABASE** statement. <mark style="background: #FF5452A6;">One consideration is to set the collation of your database so that it supports conversion of text data in files to appropriate Transact-SQL data types.</mark>

The following example code creates a database named _salesDB_ with a collation that makes it easier to import UTF-8 encoded text data into VARCHAR columns.

```sql
CREATE DATABASE SalesDB
    COLLATE Latin1_General_100_BIN2_UTF8
```

---
##### Connections
[[Creating an external data source]]
[[Creating an external file format]]
[[Encapsulate data transformations in a stored procedure]]
##### References
[Create external database objects - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/4-external-objects)