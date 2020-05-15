# Shell cmd and HDFS



##### A fency way to get distinct values:

```bash
hdfs dfs -cat /data/msd/audio/attributes/* | awk -F',' '{print $2}' | sort | uniq
```



##### Count the number of columns for each file

```bash
name=`hdfs dfs -ls /data/msd/audio/attributes/* | awk '{print $8}'`

for file in $name; do echo $file ; hdfs dfs -cat $file | wc -l; done
```

