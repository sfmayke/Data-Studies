_Tags:_ #sql
## Query clauses execution order
---
>When running a query there is a order in which the clauses are executed.

The order goes:

1. FROM
2. ON
3. JOIN
4. WHERE
5. LATEST ON
6. GROUP BY (optional)
7. WITH
8. HAVING (implicit)
9. SELECT
10. DISTINCT
11. ORDER BY
12. LIMIT
#### References
- [SQL execution order | QuestDB](https://questdb.io/docs/concept/sql-execution-order/)