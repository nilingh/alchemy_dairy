#### Create RDD

* The data should  be a [([], []), ([], []), ([], []), ...]
  * a list (df) holds tuples (rows)
  * tuple (a row) hold elements (cells/columns)

A list = [

​	([r11], [r12]),

​	([r21], [r22]),

​	...

]

* and serialize the list:

sc.parallelize(A list)

```python
In [1]: predictionAndLabels = sc.parallelize([
   ...: ...     ([1, 6, 2, 7, 8, 3, 9, 10, 4, 5], [1, 2, 3, 4, 5]),
   ...: ...     ([4, 1, 5, 6, 2, 7, 3, 8, 9, 10], [1, 2, 3]),
   ...: ...     ([1, 2, 3, 4, 5], [])])

In [2]: predictionAndLabels
Out[2]: ParallelCollectionRDD[0] at parallelize at PythonRDD.scala:195

In [3]: predictionAndLabels.collect()
Out[3]:
[([1, 6, 2, 7, 8, 3, 9, 10, 4, 5], [1, 2, 3, 4, 5]),
 ([4, 1, 5, 6, 2, 7, 3, 8, 9, 10], [1, 2, 3]),
 ([1, 2, 3, 4, 5], [])]
```



#### createDataFrame using RDD

```python
In [4]: df = spark.createDataFrame(predictionAndLabels)

In [5]: df
Out[5]: DataFrame[_1: array<bigint>, _2: array<bigint>]

In [6]: df.show()
+--------------------+---------------+
|                  _1|             _2|
+--------------------+---------------+
|[1, 6, 2, 7, 8, 3...|[1, 2, 3, 4, 5]|
|[4, 1, 5, 6, 2, 7...|      [1, 2, 3]|
|     [1, 2, 3, 4, 5]|             []|
+--------------------+---------------+
```

