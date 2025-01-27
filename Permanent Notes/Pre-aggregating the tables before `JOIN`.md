_Tags:_ #sql #sql/performance/join-optimization 
### Pre-aggregating tables before JOIN

>Useful for query optimization.

Given:
```sql
SELECT accounts.name, COUNT(*) AS web_events 
FROM accounts 
JOIN web_events events ON events.account_id = accounts.id 
GROUP BY 1 
ORDER BY 2 DESC
```

the `web_events` table has over 9.000 rows been matched to `accounts`

> [!warning]
> In queries with a `JOIN` clause, the match of the 2 tables (JOIN) is what happens first.
> See: [[Query clauses execution order]]

Now, if you extract the the `web_events` table to a [[Subquery]] to perform the aggregation before the `JOIN`, the result would give us **351** rows as result. 
Therefore when we JOIN the tables, only **351** rows would have to be evaluated:

```sql
SELECT a.name, sub.web_events 
FROM (
	SELECT account_id, COUNT(*) web_events
	FROM web_events 
	GROUP BY 1
) sub
JOIN accounts a 
ON a.id = sub.account_id 
ORDER BY 2 DESC
```