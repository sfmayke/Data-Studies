Jan 27 2025 at 15:13
_Tags:_
## Creating an external table
---
>When you need to perform a lot of analysis or reporting from files in the data lake, using <mark style="background: #FF5452A6;">the <b>OPENROWSET</b> function can result in complex code that includes data sources and file paths</mark>. To simplify access to the data, you can encapsulate the files in an external table; which users and reporting applications can query using a standard SQL SELECT statement just like any other database table.

To create an external table, use the **CREATE EXTERNAL TABLE** statement, specifying the column schema as for a standard table, and including a **WITH** clause specifying the external data source, relative path, and external file format for your data.

```sql
CREATE EXTERNAL TABLE dbo.products
(
    product_id INT,
    product_name VARCHAR(20),
    list_price DECIMAL(5,2)
)
WITH
(
    DATA_SOURCE = files,
    LOCATION = 'products/*.csv',
    FILE_FORMAT = CsvFormat
);
GO

-- query the table
SELECT * FROM dbo.products;
```

By creating a database that contains the external objects, you can <mark style="background: #ADCCFFA6;">provide a relational database layer over files in a data lake</mark>, <mark style="background: #BBFABBA6;">making it easier for many data analysts and reporting tools to access the data by using standard SQL query semantics.</mark>

---
##### Relates to
[[Create external database objects]]
##### References
[Create external database objects - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/4-external-objects)