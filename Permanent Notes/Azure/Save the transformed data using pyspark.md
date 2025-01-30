Jan 30 2025 at 09:50
_Tags:_ #pyspark #dataframe 
## Save the transformed data using pyspark
---
>After your dataFrame is in the required structure, you can save the results to a supported format in your data lake.

The following code example saves the dataFrame into a _parquet_ file in the data lake, replacing any existing file of the same name.

```python
transformed_df.write.mode("overwrite").parquet('/transformed_data/orders.parquet')
print ("Transformed data saved!")
```

>[!note] 
><mark style="background: #ADCCFFA6;">The Parquet format is typically preferred for data files that you will use for further analysis or ingestion into an analytical store.</mark> <mark style="background: #BBFABBA6;">Parquet is a very efficient format that is supported by most large scale data analytics systems.</mark> In fact, sometimes your data transformation requirement may simply be to convert data from another format (such as CSV) to Parquet!

---
##### Relates to
[[Manipulating Data frame with Spark]]
##### References
[Modify and save dataframes - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/transform-data-spark-azure-synapse-analytics/2-transform-dataframe)