_Tags:_ #sql 
## Inequality JOINs
---

> JOINs that uses comparison operators other then `=` (Equal to)

```sql
...
FROM table1
JOIN table2
ON table1.pk = table2.fk
AND table1.column1 < table2.column2
...
```