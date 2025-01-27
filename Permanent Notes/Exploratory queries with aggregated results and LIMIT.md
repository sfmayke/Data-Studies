_Tags:_ #sql #exploratory-analysis 
### Exploratory queries with aggregated results and `LIMIT` 

>When using exploratory query to investigate a large dataset, it is important to pay attention on your aggregation and `LIMIT` clause.

Since aggregations happens before `LIMIT` is applied, the query bellow would **first** aggregate the rows using `SUM` and only then limit to 10, after the most expensive calculation (`SUM`) had already been done.

```sql
SELECT SUM(column1) 
FROM table1 
WHERE occurred_at >= '2016-01-01' AND occurred_at < '2016-07-01' 
LIMIT 10
```

in other to optimize such query you can use a [[Subquery]] and apply the `LIMIT` inside it:

```sql
SELECT SUM(column1) 
FROM (SELECT * FROM table1 LIMIT 10)
WHERE occurred_at >= '2016-01-01' AND occurred_at < '2016-07-01' 
```

This way you first limit the total number of rows to then aggregate it using `SUM`.

> [!warning]
> Applying `LIMIT` on Subqueries dramatically changes the results, so use it to test queries **NOT** in the actual result.

#### Relates to 
- [[Using LIMIT and subqueries to optimize JOINs]]