Jan 27 2025 at 16:28
_Tags:_ #azure #tsql #good-practice
## Encapsulate data transformations in a stored procedure
---
>While you can run a `CREATE EXTERNAL TABLE AS SELECT` (CETAS) statement in a script whenever you need to transform data, <mark style="background: #ADCCFFA6;">it's good practice to encapsulate the transformation operation in stored procedure.</mark>

<mark style="background: #BBFABBA6;">This approach can make it easier to operationalize data transformations by enabling you to supply parameters, retrieve outputs, and include additional logic in a single procedure call.</mark>

For example, the following code creates a stored procedure that drops the external table if it already exists before recreating it with order data for the specified year:

```sql
CREATE PROCEDURE usp_special_orders_by_year @order_year INT
AS
BEGIN

	-- Drop the table if it already exists
	IF EXISTS (
                SELECT * FROM sys.external_tables
                WHERE name = 'SpecialOrders'
            )
        DROP EXTERNAL TABLE SpecialOrders

	-- Create external table with special orders
	-- from the specified year
	CREATE EXTERNAL TABLE SpecialOrders
		WITH (
			LOCATION = 'special_orders/',
			DATA_SOURCE = files,
			FILE_FORMAT = ParquetFormat
		)
	AS
	SELECT OrderID, CustomerName, OrderTotal
	FROM
		OPENROWSET(
			BULK 'sales_orders/*.csv',
			DATA_SOURCE = 'files',
			FORMAT = 'CSV',
			PARSER_VERSION = '2.0',
			HEADER_ROW = TRUE
		) AS source_data
	WHERE OrderType = 'Special Order'
	AND YEAR(OrderDate) = @order_year
END
```

##### Advantages:

- <mark style="background: #BBFABBA6;"> Reduces client to server network traffic</mark>
	- The commands in a procedure are executed as a single batch of code; which can significantly reduce network traffic between the server and client because only the call to execute the procedure is sent across the network.
- <mark style="background: #BBFABBA6;">Provides a security boundary</mark>
	- Multiple users and client programs can perform operations on underlying database objects through a procedure, even if the users and programs don't have direct permissions on those underlying objects. The procedure controls what processes and activities are performed and protects the underlying database objects; eliminating the requirement to grant permissions at the individual object level and simplifies the security layers.
- <mark style="background: #BBFABBA6;">Eases maintenance</mark>
	- Any changes in the logic or file system locations involved in the data transformation can be applied only to the stored procedure; without requiring updates to client applications or other calling functions.
- <mark style="background: #BBFABBA6;">Improved performance</mark>
	- Stored procedures are compiled the first time they're executed, and the resulting execution plan is held in the cache and reused on subsequent runs of the same stored procedure. As a result, it takes less time to process the procedure.
---
##### Relates to
[[Create external database objects]]
##### References
[Encapsulate data transformations in a stored procedure - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/use-azure-synapse-serverless-sql-pools-for-transforming-data-lake/3-operationalize-data-transformation-using-stored-procedures)