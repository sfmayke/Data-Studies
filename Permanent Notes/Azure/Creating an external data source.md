Jan 27 2025 at 14:58
_Tags:_ #tsql #azure #database 
## Creating an external data source
---
>You can use the **OPENROWSET** function with a **BULK** path to query file data from your own database, just as you can in the **master** database; but if you plan to query data in the same location frequently, <mark style="background: #ADCCFFA6;">it's more efficient to define an external data source that references that location.</mark>

For example, the following code creates a data source named _files_ for the hypothetical `https://mydatalake.blob.core.windows.net/data/files/` folder:

```sql
CREATE EXTERNAL DATA SOURCE files
WITH (
    LOCATION = 'https://mydatalake.blob.core.windows.net/data/files/'
)
```
One benefit of an external data source, is that <mark style="background: #BBFABBA6;">you can simplify an <b>OPENROWSET</b> query to use the combination of the data source and the relative path to the folders or files you want to query</mark>:

```sql
SELECT *
FROM
    OPENROWSET(
        BULK 'orders/*.csv',
        DATA_SOURCE = 'files',
        FORMAT = 'csv',
        PARSER_VERSION = '2.0'
    ) AS orders
```

Another benefit of using a data source is that <mark style="background: #BBFABBA6;">you can assign a credential for the data source to use when accessing the underlying storage, enabling you to provide access to data through SQL without permitting users to access the data directly in the storage account.</mark>

```sql
CREATE DATABASE SCOPED CREDENTIAL sqlcred
WITH
    IDENTITY='SHARED ACCESS SIGNATURE',  
    SECRET = 'sv=xxx...';
GO

CREATE EXTERNAL DATA SOURCE secureFiles
WITH (
    LOCATION = 'https://mydatalake.blob.core.windows.net/data/secureFiles/'
    CREDENTIAL = sqlcred
);
GO
```

>[!hint] or more information on storage access control via SQL: [Control storage account access for serverless SQL pool - Azure Synapse Analytics | Microsoft Learn](https://learn.microsoft.com/en-us/azure/synapse-analytics/sql/develop-storage-files-storage-access-control?tabs=user-identity)

##### Relates to
[[Create external database objects]]
##### References
[Create external database objects - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/4-external-objects)