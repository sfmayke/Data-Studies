_Tags:_ #sql #exploratory-analysis 
### Exploratory Queries

>Queries that aim the investigation of a large dataset by first analyzing a small subset of data from it.

Can be done by reducing the amount of data been searched using a `WHERE` clause:

```sql
WHERE occurred_at >= '2016-01-01' AND occurred_at < '2017-01-01'
```

and/or by using `LIMIT` :

```sql
SELECT *
FROM ...
LIMIT 10
```

> [!info]
> Some SQL editor already append a `LIMIT`  to the end of the query for exploration.

> [!warning]
> Aggregations happens before the `LIMIT` therefore there is no point on using `LIMIT` on aggregated results ( performance wise* ).
> See: [[Query clauses execution order]]