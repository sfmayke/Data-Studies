## Remainder JOIN
---
#sql 

> [!abstract] 
> _The term is coined by me.*_
> 
> Technique to know know which rows of a **JOIN** had no match. 

> [!example]
> 
> ![[remainder_join.png|200]]
> 
> ```sql
> WHERE Table_A.column_name IS NULL OR Table_B.column_name IS NULL
> ```
> 
