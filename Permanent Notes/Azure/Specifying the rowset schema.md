Jan 27 2025 at 14:21
_Tags:_ #azure #database #tsql #synapse 
## Specifying the rowset schema
---
><mark style="background: #ADCCFFA6;">It's common for delimited text files to include the column names in the first row</mark>. The **OPENROWSET** function can use this to define the schema for the resulting rowset, and <mark style="background: #CACFD9A6;">automatically infer the data types of the columns based on the values they contain</mark>.

For example, consider the following delimited text:

```text
product_id,product_name,list_price
123,Widget,12.99
124,Gadget,3.99
```

The tsql code to extract the column names properly would be:

```sql
SELECT TOP 100 *
FROM OPENROWSET(
    BULK 'https://mydatalake.blob.core.windows.net/data/files/*.csv',
    FORMAT = 'csv',
    PARSER_VERSION = '2.0',
    HEADER_ROW = TRUE) AS rows
```

The **HEADER_ROW** parameter <mark style="background: #FF5452A6;">(which is only available when using parser version 2.0) </mark>instructs the query engine to use the first row of data in each file as the column names.

For file without header you can use **WITH** to specify the file schema:

```sql
SELECT TOP 100 *
FROM OPENROWSET(
    BULK 'https://mydatalake.blob.core.windows.net/data/files/*.csv',
    FORMAT = 'csv',
    PARSER_VERSION = '2.0')
WITH (
    product_id INT,
    product_name VARCHAR(20) COLLATE Latin1_General_100_BIN2_UTF8,
    list_price DECIMAL(5,2)
) AS rows
```
##### Relates to
[[Query Files]]
##### References
[Query files using a serverless SQL pool - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/3-query-files)