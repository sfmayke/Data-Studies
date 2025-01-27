#sql
## Self JOIN
---
> Regular **JOIN** but with itself.

### Use Cases
---
#### Checking a table against itself

> [!example] 
> Imagine you want to narrow down the time between occurrences of a particular event on a ```events``` table, getting all events that occurred within 2 days from one another:
> ```sql 
> events.occurred_at < events.occurred_at - INTERVAL('2 days') 
> ```
> The second argument cant be the same column been iterated over, you will need to use the same table under another alias:
> ```sql
> ...
> FROM events t1
> JOIN events t2
> ON t1.id = t2.id
>AND t1.occurred_at < t2.occurred_at - INTERVAL('2 days')
>...
> ```
> In this situation although we are looking at the same column, we are not looking at the same table.
> 
> >[!info]
>Commonly used on [[Inequality JOINs]]



