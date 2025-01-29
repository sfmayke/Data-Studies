Jan 28 2025 at 13:57
_Tags:_ #azure #delta_lake #synapse 
## Delta Lake
---
>Delta Lake is an open-source storage layer that adds relational database semantics to Spark-based data lake processing. Delta Lake is supported in Azure Synapse Analytics Spark pools for PySpark, Scala, and .NET code.

The benefits of using Delta Lake in a Synapse Analytics Spark pool include:

- <mark style="background: #BBFABBA6;"><b>Relational tables that support querying and data modification</b>. </mark>With Delta Lake, you can store data in tables that support _CRUD_ (create, read, update, and delete) operations. In other words, you can _select_, _insert_, _update_, and _delete_ rows of data in the same way you would in a relational database system.
- <mark style="background: #BBFABBA6;"><b>Support for _ACID_ transactions</b></mark>. Relational databases are designed to support transactional data modifications that provide _atomicity_ (transactions complete as a single unit of work), _consistency_ (transactions leave the database in a consistent state), _isolation_ (in-process transactions can't interfere with one another), and _durability_ (when a transaction completes, the changes it made are persisted). Delta Lake brings this same transactional support to Spark by implementing a transaction log and enforcing serializable isolation for concurrent operations.
- <mark style="background: #BBFABBA6;"><b>Data versioning and _time travel_</b>.</mark> Because all transactions are logged in the transaction log, you can track multiple versions of each table row and even use the _time travel_ feature to retrieve a previous version of a row in a query.
- <mark style="background: #BBFABBA6;"><b>Support for batch and streaming data</b>. </mark>While most relational databases include tables that store static data, Spark includes native support for streaming data through the Spark Structured Streaming API. Delta Lake tables can be used as both _sinks_ (destinations) and _sources_ for streaming data.
- <mark style="background: #BBFABBA6;"><b>Standard formats and interoperability</b>.</mark> The underlying data for Delta Lake tables is stored in Parquet format, which is commonly used in data lake ingestion pipelines. Additionally, you can use the serverless SQL pool in Azure Synapse Analytics to query Delta Lake tables in SQL.
---
##### Connects to
[[Create Delta Lake tables]]
##### References
[Understand Delta Lake - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/use-delta-lake-azure-synapse-analytics/2-understand-delta-lake)