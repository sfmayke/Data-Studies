Jan 27 2025 at 13:53
_Tags:_ #tsql #synapse #azure 
## Query Files
---
>You can <mark style="background: #ADCCFFA6;">use a serverless SQL pool to query data files</mark> in various common file formats

- Delimited text, such as comma-separated values (CSV) files.
- JavaScript object notation (JSON) files.
- Parquet files.

<mark style="background: #BBFABBA6;">The basic syntax for querying is the same for all of these types of file, and is built on the OPENROWSET SQL function</mark>; <mark style="background: #CACFD9A6;">which generates a tabular rowset from data in one or more files</mark>. For example, the following query could be used to extract data from CSV files.

```sql
SELECT TOP 100 *
FROM OPENROWSET(
    BULK 'https://mydatalake.blob.core.windows.net/data/files/*.csv',
    FORMAT = 'csv') AS rows
```

The OPENROWSET function includes more parameters that determine factors such as:

- The schema of the resulting rowset
- Additional formatting options for delimited text files.

<mark style="background: #ADCCFFA6;">The output from <b>OPENROWSET</b> is a rowset to which an alias must be assigned</mark>. In the previous example, the alias **rows** is used to name the resulting rowset.

<mark style="background: #ADCCFFA6;">The <b>BULK</b> parameter includes the full URL to the location in the data lake containing the data files</mark>. This can be an individual file, or a folder with a wildcard expression to filter the file types that should be included. The **FORMAT** parameter specifies the type of data being queried. The example above reads delimited text from all .csv files in the **files** folder.

##### Connections
[[Querying delimited text files]]
[[Specifying the rowset schema]]
[[Query partitioned data]]
[[Querying Parquet files]]
[[Querying JSON files]]
##### References
[How to use OPENROWSET in serverless SQL pool - Azure Synapse Analytics | Microsoft Learn](https://learn.microsoft.com/en-us/azure/synapse-analytics/sql/develop-openrowset#syntax)

