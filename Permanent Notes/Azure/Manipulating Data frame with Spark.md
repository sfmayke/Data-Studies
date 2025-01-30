Jan 30 2025 at 09:44
_Tags:_ #pyspark #dataframe
## Manipulating Dataframe with Spark
---
>Apache Spark provides the _dataframe_ object as the primary structure for working with data. <mark style="background: #ADCCFFA6;">You can use dataframes to query and transform data, and persist the results in a data lake.</mark>

To load data into a dataframe, you use the **spark.read** function, specifying the file format, path, and optionally the schema of the data to be read. For example, the following code loads data from all .csv files in the **orders** folder into a dataframe named **order_details** and then displays the first five records.

```sql
order_details = spark.read.csv('/orders/*.csv', header=True, inferSchema=True)
display(order_details.limit(5))
```
---
##### Connects to
[[Transform the data structure using pyspark]]
[[Save the transformed data using pyspark]]
[[Partition data files with pyspark]]
##### References
[Modify and save dataframes - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/transform-data-spark-azure-synapse-analytics/2-transform-dataframe)