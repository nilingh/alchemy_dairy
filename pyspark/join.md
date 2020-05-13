##### Join between two data frames

* `left/right/full` = `left_outer/right_outer/full_outer`
* `left_semi` keeps matched rows in the left data set
* `left_anti` keeps **not** matched rows in the left data set

Here is the example code:

```python
schema = StructType([
	StructField("ID", StringType(), True),
	StructField("VALUE", StringType(), True),
	StructField("ADD", StringType(), True)
])

data_left = spark.createDataFrame(
	sc.parallelize( # python object representing on RDD[Row]
		[
        ("1","A1","L1"), # python list of rows in python (on the master node)
		("2","A2","L2"),
		("3","A3","L3"),
		("4","A4","L4")		
        ]
    ), schema=schema)


data_right = spark.createDataFrame(
	sc.parallelize( # python object representing on RDD[Row]
		[
        ("3","A3","L3"), # python list of rows in python (on the master node)
		("4","A4","L4"),
		("4","A4_1","L4_1"),
		("5","A5","L5"),
		("6","A6","L6")
        ]
    ), schema=schema)

join_types = ["inner",  "left", "left_outer",  "left_semi", "left_anti","right","right_outer","outer", "full", "full_outer"]

data_left.show()

data_right.show()

for join_type in join_types:
	print("Join type is: {}".format(join_type))
	data_left.join(data_right, on="ID", how=join_type).orderBy("ID").show()
    

    ...:
+---+-----+---+
| ID|VALUE|ADD|
+---+-----+---+
|  1|   A1| L1|
|  2|   A2| L2|
|  3|   A3| L3|
|  4|   A4| L4|
+---+-----+---+

+---+-----+----+
| ID|VALUE| ADD|
+---+-----+----+
|  3|   A3|  L3|
|  4|   A4|  L4|
|  4| A4_1|L4_1|
|  5|   A5|  L5|
|  6|   A6|  L6|
+---+-----+----+

Join type is: inner
+---+-----+---+-----+----+
| ID|VALUE|ADD|VALUE| ADD|
+---+-----+---+-----+----+
|  3|   A3| L3|   A3|  L3|
|  4|   A4| L4|   A4|  L4|
|  4|   A4| L4| A4_1|L4_1|
+---+-----+---+-----+----+

Join type is: left
+---+-----+---+-----+----+
| ID|VALUE|ADD|VALUE| ADD|
+---+-----+---+-----+----+
|  1|   A1| L1| null|null|
|  2|   A2| L2| null|null|
|  3|   A3| L3|   A3|  L3|
|  4|   A4| L4|   A4|  L4|
|  4|   A4| L4| A4_1|L4_1|
+---+-----+---+-----+----+

Join type is: left_outer
+---+-----+---+-----+----+
| ID|VALUE|ADD|VALUE| ADD|
+---+-----+---+-----+----+
|  1|   A1| L1| null|null|
|  2|   A2| L2| null|null|
|  3|   A3| L3|   A3|  L3|
|  4|   A4| L4| A4_1|L4_1|
|  4|   A4| L4|   A4|  L4|
+---+-----+---+-----+----+

Join type is: left_semi
+---+-----+---+
| ID|VALUE|ADD|
+---+-----+---+
|  3|   A3| L3|
|  4|   A4| L4|
+---+-----+---+

Join type is: left_anti
+---+-----+---+
| ID|VALUE|ADD|
+---+-----+---+
|  1|   A1| L1|
|  2|   A2| L2|
+---+-----+---+

Join type is: right
+---+-----+----+-----+----+
| ID|VALUE| ADD|VALUE| ADD|
+---+-----+----+-----+----+
|  3|   A3|  L3|   A3|  L3|
|  4|   A4|  L4|   A4|  L4|
|  4|   A4|  L4| A4_1|L4_1|
|  5| null|null|   A5|  L5|
|  6| null|null|   A6|  L6|
+---+-----+----+-----+----+

Join type is: right_outer
+---+-----+----+-----+----+
| ID|VALUE| ADD|VALUE| ADD|
+---+-----+----+-----+----+
|  3|   A3|  L3|   A3|  L3|
|  4|   A4|  L4|   A4|  L4|
|  4|   A4|  L4| A4_1|L4_1|
|  5| null|null|   A5|  L5|
|  6| null|null|   A6|  L6|
+---+-----+----+-----+----+

Join type is: outer
+---+-----+----+-----+----+
| ID|VALUE| ADD|VALUE| ADD|
+---+-----+----+-----+----+
|  1|   A1|  L1| null|null|
|  2|   A2|  L2| null|null|
|  3|   A3|  L3|   A3|  L3|
|  4|   A4|  L4|   A4|  L4|
|  4|   A4|  L4| A4_1|L4_1|
|  5| null|null|   A5|  L5|
|  6| null|null|   A6|  L6|
+---+-----+----+-----+----+

Join type is: full
+---+-----+----+-----+----+
| ID|VALUE| ADD|VALUE| ADD|
+---+-----+----+-----+----+
|  1|   A1|  L1| null|null|
|  2|   A2|  L2| null|null|
|  3|   A3|  L3|   A3|  L3|
|  4|   A4|  L4|   A4|  L4|
|  4|   A4|  L4| A4_1|L4_1|
|  5| null|null|   A5|  L5|
|  6| null|null|   A6|  L6|
+---+-----+----+-----+----+

Join type is: full_outer
+---+-----+----+-----+----+
| ID|VALUE| ADD|VALUE| ADD|
+---+-----+----+-----+----+
|  1|   A1|  L1| null|null|
|  2|   A2|  L2| null|null|
|  3|   A3|  L3|   A3|  L3|
|  4|   A4|  L4| A4_1|L4_1|
|  4|   A4|  L4|   A4|  L4|
|  5| null|null|   A5|  L5|
|  6| null|null|   A6|  L6|
+---+-----+----+-----+----+
```

