### Commands to run in the Spark terminal

to start the Spark terminal: `spark-shell`

```
scala> val data = sc.textFile("swati/sparkdata.txt")
data: org.apache.spark.rdd.RDD[String] = swati/sparkdata.txt MapPartitionsRDD[1] at textFile at <console>:24
```

```
scala> data.collect;
res0: Array[String] = Array(hello world, this is BDA spark lab)
```

```
scala> val splitdata = data.flatMap(line => line.split(" "));
splitdata: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[2] at flatMap at <console>:25
```

```
scala> splitdata.collect;
res1: Array[String] = Array(hello, world,, this, is, BDA, spark, lab)
```

```
scala> val mapdata = splitdata.map(word => (word,1));
mapdata: org.apache.spark.rdd.RDD[(String, Int)] = MapPartitionsRDD[3] at map at <console>:25
```

```
scala> mapdata.collect;
res2: Array[(String, Int)] = Array((hello,1), (world,,1), (this,1), (is,1), (BDA,1), (spark,1), (lab,1))
```

```
scala> val reducedata = mapdata.reduceByKey(_+_);
reducedata: org.apache.spark.rdd.RDD[(String, Int)] = ShuffledRDD[4] at reduceByKey at <console>:25
```

```
scala> reducedata.collect;
res3: Array[(String, Int)] = Array((this,1), (is,1), (hello,1), (world,,1), (lab,1), (spark,1), (BDA,1))
```


