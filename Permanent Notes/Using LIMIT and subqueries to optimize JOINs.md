_Tags:_ #sql #sql/performance/join-optimization
### Using LIMIT and subqueries to optimize JOINs

>You can optimize JOINs by limiting the results of a table before the JOIN is executed using a subquery:

```sql
SELECT column1, SUM(column2) 
FROM table1 
JOIN tabl2
GROUP BY 1
LIMIT 10
```

> [!warning]
> The `JOIN` will be executed first is the query above then the result would be limited. 
> See: [[Query clauses execution order]]

The `SUM` would happens first, running over all rows of the table, then it would limit the result to 10.
In order to avoid this you can first limit the table rows using a [[Subquery]] then applying the aggregation on top of that limited result:

```sql
SELECT sub.column1, SUM(table2.column2) 
FROM (SELECT * FROM table1 LIMIT 10) sub
JOIN table2
GROUP BY 1
```

Both the `JOIN` and aggregation will now happens on top of a limited `table1`  making both processes much faster.

> [!info] 
> Normally used on [[Exploratory queries with aggregated results and LIMIT]]