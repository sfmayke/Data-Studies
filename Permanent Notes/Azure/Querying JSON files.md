Jan 27 2025 at 14:28
_Tags:_ #azure #tsql #synapse 
## Querying JSON files
---
>JSON is a <mark style="background: #ADCCFFA6;">popular format for web applications that exchange data through REST interfaces or use NoSQL data stores such as Azure Cosmos DB</mark>. So, it's not uncommon to persist data as JSON documents in files in a data lake for analysis.

For example, a JSON file that defines an individual product might look like this:

```json
{
    "product_id": 123,
    "product_name": "Widget",
    "list_price": 12.99
}
```

To return product data from a folder containing multiple JSON files in this format, you could use the following SQL query:

```sql
SELECT doc
FROM
    OPENROWSET(
        BULK 'https://mydatalake.blob.core.windows.net/data/files/*.json',
        FORMAT = 'csv',
        FIELDTERMINATOR ='0x0b',
        FIELDQUOTE = '0x0b',
        ROWTERMINATOR = '0x0b'
    ) WITH (doc NVARCHAR(MAX)) as rows
```

<mark style="background: #FF5452A6;"><b>OPENROWSET</b> has no specific format for JSON files</mark>, so you must use _csv_ format with **FIELDTERMINATOR**, **FIELDQUOTE**, and **ROWTERMINATOR** set to _0x0b_, and a schema that includes a single **NVARCHAR(MAX)** column. The result of this query is a rowset containing a single column of JSON documents, like this:

| doc                                                            |
| -------------------------------------------------------------- |
| {"product_id":123,"product_name":"Widget","list_price": 12.99} |
| {"product_id":124,"product_name":"Gadget","list_price": 3.99}  |

To extract individual values from the **JSON**, you can use the **JSON_VALUE** function in the **SELECT** statement, as shown here:

```sql
SELECT JSON_VALUE(doc, '$.product_name') AS product,
           JSON_VALUE(doc, '$.list_price') AS price
FROM
    OPENROWSET(
        BULK 'https://mydatalake.blob.core.windows.net/data/files/*.json',
        FORMAT = 'csv',
        FIELDTERMINATOR ='0x0b',
        FIELDQUOTE = '0x0b',
        ROWTERMINATOR = '0x0b'
    ) WITH (doc NVARCHAR(MAX)) as rows
```

This query would return a rowset similar to the following results:

| product | price |
| ------- | ----- |
| Widget  | 12.99 |
| Gadget  | 3.99  |

---
##### Relates to
[[Query Files]]
##### References
[Query files using a serverless SQL pool - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/3-query-files)