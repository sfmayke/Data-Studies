Jan 27 2025 at 15:09
_Tags:_ #azure #synapse #tsql 
## Creating an external file format
---
>While an external data source simplifies the code needed to access files with the **OPENROWSET** function, <mark style="background: #ADCCFFA6;">you still need to provide format details for the file being access;</mark> which may include multiple settings for delimited text files.

You can encapsulate these settings in an external file format, like this:

```sql
CREATE EXTERNAL FILE FORMAT CsvFormat
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS(
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '"'
        )
    );
GO
```

---
##### Relates to
[[Create external database objects]]
##### References
[Create external database objects - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/query-data-lake-using-azure-synapse-serverless-sql-pools/4-external-objects)