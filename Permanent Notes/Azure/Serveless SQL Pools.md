Jan 27 2025 at 10:38
_Tags: #serverless #sql

## Serverless SQL Pools
---
>On-demand SQL query processing, primarily used to work with data in a data lake
>
>Serverless SQL pool is tailored for querying the data residing in the data lake, so in addition to eliminating management burden, it eliminates a need to worry about ingesting the data into the system. You just point the query to the data that is already in the lake and run it.

Synapse SQL serverless resource model <mark style="background: #ADCCFFA6;">is great for unplanned or "bursty" workloads</mark> that can be processed <mark style="background: #CACFD9A6;">using the always-on serverless SQL endpoint</mark> in your Azure Synapse Analytics workspace.

>[!info]
>Serverless SQL pool is an analytics system and <mark style="background: #FF5452A6;">is not recommended for OLTP workloads</mark> such as databases used by applications to store transactional data. Workloads that require millisecond response times and are looking to pinpoint a single row in a data set are not good fit for serverless SQL pool.

#### The benefits of using serverless SQL pool

- <mark style="background: #BBFABBA6;">A familiar Transact-SQL syntax</mark> to query data in place without the need to copy or load data into a specialized store.
- <mark style="background: #BBFABBA6;">Integrated connectivity</mark> from a wide range of business intelligence and ad-hoc querying tools, including the most popular drivers.
- <mark style="background: #BBFABBA6;">Distributed query processing</mark> that is built for large-scale data, and computational functions - resulting in fast query performance.
- <mark style="background: #BBFABBA6;">Built-in query execution fault-tolerance</mark>, resulting in high reliability and success rates even for long-running queries involving large data sets.
- <mark style="background: #BBFABBA6;">No infrastructure to setup or clusters to maintain</mark>. A built-in endpoint for this service is provided within every Azure Synapse workspace, so you can start querying data as soon as the workspace is created.
- <mark style="background: #BBFABBA6;">No charge for resources reserved</mark>, you're only charged for the data processed by queries you run.
#### Use cases for serverless SQL pools

- **Data exploration**: Data exploration involves browsing the data lake to get initial insights about the data, and is easily achievable with Azure Synapse Studio. You can browse through the files in your linked data lake storage, and use the built-in serverless SQL pool to automatically generate a SQL script to select TOP 100 rows from a file or folder just as you would do with a table in SQL Server. From there, <mark style="background: #CACFD9A6;">you can apply projections, filtering, grouping, and most of the operation over the data as if the data were in a regular SQL Server table.</mark>
- **Data transformation**: While Azure Synapse Analytics provides great data transformations capabilities with Synapse Spark, some data engineers might find data transformation easier to achieve using SQL. <mark style="background: #BBFABBA6;">Serverless SQL pool enables you to perform SQL-based data transformations</mark>; either interactively or as part of an automated data pipeline.
- **Logical data warehouse**: After your initial exploration of the data in the data lake, you can define external objects such as tables and views in a serverless SQL database. <mark style="background: #ADCCFFA6;">The data remains stored in the data lake files</mark>, but are <mark style="background: #CACFD9A6;">abstracted by a relational schema</mark> that can be used by client applications and analytical tools to query the data as they would in a relational database hosted in SQL Server.

##### Relates to

##### References
[Understand Azure Synapse serverless SQL pool capabilities and use cases - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/2-understand-serverless-pools)