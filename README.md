# spark-wordcount-example

> 此repository是[Apache Mesos(10)-使用Chronos创建复杂任务](https://andyyoung01.github.io/2016/08/05/Apache-Mesos-10-使用Chronos创建复杂任务/)的示例代码。对Mesos in Action的[wordcount-example](https://github.com/rji/mesos-in-action-code-samples/tree/master/wordcount-example)的代码进行了小的变动。

This is an example Spark job that reads a copy of Leo Tolstoy's
[War and Peace][war-and-peace-pg] from HDFS, counts the number of times each
word appears, then stores the word counts in a text file (also on HDFS). This
is meant to be used with the Chronos jobs located at `../complex-etl-job`.

## Usage
Clone the repo and package up the example:

```
$ git clone https://github.com/andyyoung01/spark-wordcount.git
$ cd spark-wordcount/wordcount-example
$ sbt package
```

Assuming the `spark-submit` utility is available on the `$PATH` of your gateway
machine, submit the job by running the following command:

```
$ spark-submit target/scala-2.10/war-and-peace-wordcount_2.10-0.1.0-SNAPSHOT.jar \
  /tmp/warandpeace
```

## Results
The results of the job can then be found on HDFS at
`${basepath}/warandpeace-counts.txt`. You can get the top 10 words in the book
by running the following command:

```
$ hadoop fs -cat /tmp/warandpeace/warandpeace-counts.txt/part-* | sort -t, -rnk2 | head -10
(the,34570)
(and,22159)
(to,16716)
(of,14991)
(,13568)
(a,10521)
(he,9809)
(in,8801)
(his,7967)
(that,7813)
```

## Reference
  * [Installing SBT on Linux][sbt-install-linux]
  * [Spark Downloads][spark-downloads]
  * [Installing CDH 5.3 with MRv1 on a Single Linux Node][cdh5-single-node]
  * [Installing and Deploying CDH 5.3 Using the Command Line][cdh5-install-docs]


[war-and-peace-pg]: http://www.gutenberg.org/files/2600/2600-0.txt
[sbt-install-linux]: http://www.scala-sbt.org/0.13/tutorial/Installing-sbt-on-Linux.html
[spark-downloads]: http://spark.apache.org/downloads.html
[cdh5-single-node]: http://www.cloudera.com/content/www/en-us/documentation/enterprise/5-3-x/topics/cdh_qs_mrv1_pseudo.html
[cdh5-install-docs]: http://www.cloudera.com/content/www/en-us/documentation/enterprise/5-3-x/topics/cdh_ig_command_line.html