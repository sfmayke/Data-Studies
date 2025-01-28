Jan 27 2025 at 14:44
_Tags:_ #tsql #azure #synapse 
## Query partitioned data
---
<mark style="background: #ADCCFFA6;">>It's common in a data lake to partition data by splitting across multiple files in subfolders that reflect partitioning criteria</mark>. <mark style="background: #BBFABBA6;">This enables distributed processing systems to work in parallel on multiple partitions of the data, or to easily eliminate data reads from specific folders based on filtering criteria.</mark>

For example, suppose you need to efficiently process sales order data, and often need to filter based on the year and month in which orders were placed. You could partition the data using folders, like this:

- /orders
    - /year=2020
        - /month=1
            - /01012020.parquet
            - /02012020.parquet
            - ...
        - /month=2
            - /01022020.parquet
            - /02022020.parquet
            - ...
        - ...
    - /year=2021
        - /month=1
            - /01012021.parquet
            - /02012021.parquet
            - ...
        - ...

To create a query that filters the results to include only the orders for January and February 2020, you could use the following code:

```sql
SELECT *
FROM OPENROWSET(
    BULK 'https://mydatalake.blob.core.windows.net/data/orders/year=*/month=*/*.*',
    FORMAT = 'parquet') AS orders
WHERE orders.filepath(1) = '2020'
    AND orders.filepath(2) IN ('1','2');
```
---
##### Relates to
[[Query Files]]
##### References
[Query files using a serverless SQL pool - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/3-query-files)