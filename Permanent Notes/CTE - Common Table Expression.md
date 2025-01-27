_tags:_ #sql
### CTE - Common Table Expression

It is a **SQL**  construct used to create a _virtual_ table that exists only during the execution of a query.

```sql
WITH table_name AS (
	SELECT * 
	FROM table1
	...
)
SELECT * FROM table_name;
```

> [!tip]
> Very useful to avoid unnecessary redundancy, since the `table_name` used can be referenced later in the main query.