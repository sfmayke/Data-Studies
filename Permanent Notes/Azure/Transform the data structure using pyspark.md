Jan 30 2025 at 09:47
_Tags:_ #pyspark #dataframe
## Transform the data structure using pyspark
---
>After loading the source data into a dataframe, you can use the dataframe object's methods and Spark functions to transform it.

Typical operations on a dataframe include:

- Filtering rows and columns
- Renaming columns
- Creating new columns, often derived from existing ones
- Replacing null or other values

In the following example, the code uses the `split` function to separate the values in the **CustomerName** column into two new columns named **FirstName** and **LastName**. Then it uses the `drop` method to delete the original **CustomerName** column.

```sql
from pyspark.sql.functions import split, col

# Create the new FirstName and LastName fields
transformed_df = order_details.withColumn("FirstName", split(col("CustomerName"), " ").getItem(0)).withColumn("LastName", split(col("CustomerName"), " ").getItem(1))

# Remove the CustomerName field
transformed_df = transformed_df.drop("CustomerName")

display(transformed_df.limit(5))
```

---
##### Relates to
[[Manipulating Data frame with Spark]]
##### References
[Modify and save dataframes - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/transform-data-spark-azure-synapse-analytics/2-transform-dataframe)