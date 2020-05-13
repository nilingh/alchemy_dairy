##### What is  `spark.read()` ?

*class* `pyspark.sql.DataFrameReader`(*spark*)[[source\]](https://spark.apache.org/docs/latest/api/python/_modules/pyspark/sql/readwriter.html#DataFrameReader)

Interface used to load a [`DataFrame`](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html#pyspark.sql.DataFrame) from external storage systems (e.g. file systems, key-value stores, etc). Use `spark.read()` to access this.

##### Load text file

1. [**text**(*paths*, *wholetext=False*, *lineSep=None*)](https://spark.apache.org/docs/latest/api/python/_modules/pyspark/sql/readwriter.html#DataFrameReader.text) 

   目前支持3个参数，*wholetext*可将文本导入成一个cell

```python
df = spark.read.text("hdfs:///data/msd/tasteprofile/mismatches/sid_msimatches.txt")
```

2. format("text").option().load()

   Data sources are specified by their fully qualified name (i.e., `org.apache.spark.sql.parquet`), but for built-in sources you can also use their short names (`json`, `parquet`, `jdbc`, `orc`, `libsvm`, `csv`, `text`)

```python
df = (
    spark.read.format("text")
    .load("hdfs:///data/msd/tasteprofile/mismatches/sid_msimatches.txt")
```

官方文档中有些option不全，比如`.option("recursiveFileLookup", "true")`。更多例子如下：

[Generic Load/Save Functions](https://spark.apache.org/docs/latest/sql-data-sources-load-save-functions.html)

[Find full example code in the Spark repo](https://github.com/apache/spark/blob/master/examples/src/main/python/sql/datasource.py)

