Jan 27 2025 at 14:00
_Tags:_ #tsql #azure #synapse 
## Querying delimited text files
---
>Delimited text files are a common file format within many businesses. The specific formatting used in delimited files can vary.

- With and without a header row.
- Comma and tab-delimited values.
- Windows and Unix style line endings.
- Non-quoted and quoted values, and escaping characters.

Regardless of the type of delimited file you're using, <mark style="background: #ADCCFFA6;">you can read data from them by using the OPENROWSET function with the <b>csv</b> FORMAT parameter</mark>, and other parameters as required to handle the specific formatting details for your data. For example:

```sql
SELECT TOP 100 *
FROM OPENROWSET(
    BULK 'https://mydatalake.blob.core.windows.net/data/files/*.csv',
    FORMAT = 'csv',
    PARSER_VERSION = '2.0',
    FIRSTROW = 2) AS rows
```

<mark style="background: #ADCCFFA6;">The PARSER_VERSION is used to determine how the query interprets the text encoding used in the files</mark>. Version 1.0 is the default and supports a wide range of file encodings, while <mark style="background: #BBFABBA6;">version 2.0 supports fewer encodings but offers better performance</mark>. The **FIRSTROW** parameter is used to skip rows in the text file, to eliminate any unstructured preamble text or to ignore a row containing column headings.

>[!tip]
>For details of additional parameters when working with delimited text files, refer to the [Azure Synapse Analytics documentation](https://learn.microsoft.com/en-us/azure/synapse-analytics/sql/develop-openrowset#syntax).

##### Relates to
[[Query Files]]
##### References
[Query files using a serverless SQL pool - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/3-query-files)