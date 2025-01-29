Jan 29 2025 at 13:42
_Tags:_
## Create catalog tables
---
>You can also define Delta Lake tables as catalog tables in the Hive metastore for your Spark pool, and work with them using SQL.

#####  External vs Managed tables

Tables in a Spark catalog, including Delta Lake tables, can be _managed_ or _external_; and it's important to understand the distinction between these kinds of table.

- A _managed_ table is defined without a specified location, and the <mark style="background: #CACFD9A6;">data files are stored within the storage used by the metastore</mark>. <mark style="background: #FF5452A6;">Dropping the table not only removes its metadata from the catalog, but also deletes the folder in which its data files are stored.</mark>
- An _external_ table is defined for a custom file location, where the data for the table is stored. The metadata for the table is defined in the Spark catalog. <mark style="background: #ADCCFFA6;">Dropping the table deletes the metadata from the catalog, but doesn't affect the data files.</mark>

##### Creating a catalog table from a dataframe

You can create managed tables by writing a dataframe using the `saveAsTable` operation as shown in the following examples:

```sql
# Save a dataframe as a managed table
df.write.format("delta").saveAsTable("MyManagedTable")

## specify a path option to save as an external table
df.write.format("delta").option("path", "/mydata").saveAsTable("MyExternalTable")
```

---
##### Relates to

##### References
