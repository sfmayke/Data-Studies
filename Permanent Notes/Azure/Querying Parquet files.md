Jan 27 2025 at 14:39
_Tags:_ #azure #synapse #tsql
## Querying Parquet files
---
>Parquet is a commonly used format for big data processing on distributed file storage. I<mark style="background: #BBFABBA6;">t's an efficient data format that is optimized for compression and analytical querying.</mark>

In most cases, the schema of the data is embedded within the Parquet file, so you only need to specify the **BULK** parameter with a path to the file(s) you want to read, and a **FORMAT** parameter of _parquet_; like this:

```sql
SELECT TOP 100 *
FROM OPENROWSET(
    BULK 'https://mydatalake.blob.core.windows.net/data/files/*.*',
    FORMAT = 'parquet') AS rows
```

---
##### Relates to
[[Query Files]]
##### References
[Query files using a serverless SQL pool - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/3-query-files)