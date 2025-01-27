_Tags:_ #sql
### SQL PARTITION

>In order to make a aggregation but keeping the rows of the result you need a [[SQL Window function]].

The `PARTITION BY` clause will allow you to aggregated a result without having to collapse the rows:

```sql
AGGREGATION_FUNCTION(table_column1) OVER (PARTITION BY table_column2) as column_name
```

In the snippet above `table_column1`represent the column you are aggregating and `table_column2` the "window"in which the aggregation is taking place.