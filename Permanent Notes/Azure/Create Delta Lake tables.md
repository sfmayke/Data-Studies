Jan 28 2025 at 14:02
_Tags:_ #azure #synapse #delta_lake 
## Create Delta Lake tables
---
>Delta lake is built on tables, which provide a relational storage abstraction over files in a data lake.

##### Creating a Delta Lake table from a dataframe

One of the easiest ways to create a Delta Lake table is to save a dataframe in the _delta_ format, specifying a path where the data files and related metadata information for the table should be stored.

```python
# Load a file into a dataframe
df = spark.read.load('/data/mydata.csv', format='csv', header=True)

# Save the dataframe as a delta table
delta_table_path = "/delta/mydata"
df.write.format("delta").save(delta_table_path)
```

After saving the delta table, the path location you specified includes parquet files for the data (regardless of the format of the source file you loaded into the dataframe) and a **delta_log** folder containing the transaction log for the table.

>[!note] 
>The transaction log records all data modifications to the table. <mark style="background: #BBFABBA6;">By logging each modification, transactional consistency can be enforced and versioning information for the table can be retained.</mark>

You can replace an existing Delta Lake table with the contents of a dataframe by using the **overwrite** mode, as shown here:

```python
new_df.write.format("delta").mode("overwrite").save(delta_table_path)
```

You can also add rows from a dataframe to an existing table by using the **append** mode:

```python
new_rows_df.write.format("delta").mode("append").save(delta_table_path)
```

##### Relates to
[[Delta Lake]]
##### References
