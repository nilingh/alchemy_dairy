#### What is  `spark.read()` ?

*class* `pyspark.sql.DataFrameReader`(*spark*)[[source\]](https://spark.apache.org/docs/latest/api/python/_modules/pyspark/sql/readwriter.html#DataFrameReader)

Interface used to load a [`DataFrame`](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html#pyspark.sql.DataFrame) from external storage systems (e.g. file systems, key-value stores, etc). Use `spark.read()` to access this.



#### Load text file

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



#### Schema

**schema** – a [`pyspark.sql.types.StructType`](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html#pyspark.sql.types.StructType) object or a DDL-formatted string (For example `col0 INT, col1 DOUBLE`).

1. DDL-formatted string

```python
>>> s = spark.read.schema("col0 STRING	, col1 DOUBLE")
```

2.  [`pyspark.sql.types.StructType`](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html#pyspark.sql.types.StructType) object

```python
>>> s = (spark.read.schema(StructType([
									StructField("col0", StringType()),
                  StructField("col1", DoubleType())
                  ])
               ))
```



#### Build schema from a file

![image-20200514201711446](/Users/neil/Library/Application Support/typora-user-images/image-20200514201711446.png)



#### Using Python to load a txt file

Raw file: (Million Song Dataset - mismatches)

![image-20200514200635163](/Users/neil/Library/Application Support/typora-user-images/image-20200514200635163.png)

Example code:

![image-20200514200852559](/Users/neil/Library/Application Support/typora-user-images/image-20200514200852559.png)

