
_Tags:_ #sql 
##  SQL UNION
---
>Used to create a _SET_ result ( result of the 2 tables minus duplicated rows ).
>In order to work you need tables with same **structure/data_type**, so that your **SELECT** closure matches.

```sql
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
UNION
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
```

> [!tip] Insight
> UNION is useful when you need to work with data spreed across multiple tables.

> [!info]
> If you dont wanna to remove duplicates use UNION ALL

#### Relates to

#### References
- [SQL: UNION Operator (techonthenet.com)](https://www.techonthenet.com/sql/union.php)