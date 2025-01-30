Jan 30 2025 at 09:54
_Tags:_ #pyspark #dataframe 
## Partition data files with pyspark
---
<mark style="background: #BBFABBA6;">>Partitioning is an optimization technique that enables spark to maximize performance across the worker nodes.</mark> <mark style="background: #CACFD9A6;">More performance gains can be achieved when filtering data in queries by eliminating unnecessary disk IO.</mark>

##### Partition the output file

To save a dataframe as a partitioned set of files, use the **partitionBy** method when writing the data.

The following example creates a derived **Year** field. Then uses it to partition the data.

```python
from pyspark.sql.functions import year, col

# Load source data
df = spark.read.csv('/orders/*.csv', header=True, inferSchema=True)

# Add Year column
dated_df = df.withColumn("Year", year(col("OrderDate")))

# Partition by year
dated_df.write.partitionBy("Year").mode("overwrite").parquet("/data")
```

<mark style="background: #ADCCFFA6;">The folder names generated when partitioning a dataframe include the partitioning column name and value in a _**column=value**_ format</mark>, as shown here:

![[Pasted image 20250130095540.png]]

>[!note] 
>You can partition the data by multiple columns, <mark style="background: #CACFD9A6;">which results in a hierarchy of folders for each partitioning key.</mark> For example, you could partition the order in the example by year and month, so that the folder hierarchy includes a folder for each year value, which in turn contains a subfolder for each month value.

---
##### Relates to

##### References
