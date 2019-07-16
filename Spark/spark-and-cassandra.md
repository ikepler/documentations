# Spark and Cassandra

## The Connector :link:

Using Cassandra as a data source is easily reachable with [spark-cassandra-connector](https://github.com/datastax/spark-cassandra-connector). It should be loaded with `--packages` flag on Spark worker process running or as a default package on building a session.

## With PySpark :yum:

To load the connector package on a PySpark session, you could run its command with packages flag and the connector package namespace. For example it could be like `pyspark --packages com.datastax.spark:spark-cassandra-connector_2.11:2.3.2`. You can see the [spark-cassandra-connector](https://github.com/datastax/spark-cassandra-connector) for selecting a proper version of driver based on your Spark version.

## And RStudio :bar_chart:

Similar to the previous section, you should load the connector package. It could be ran similar to the previous section with a packages flag on running `SparkR` command, or even better, making it on `SparkSession` handling section. The later can be done with adding this attribution to the Spark configurations:

```R
config$sparklyr.defaultPackages = "com.datastax.spark:spark-cassandra-connector_2.11:2.3.2"
```

Similar to the previous section, you should seek for a proper version of the driver.

## Cassandra as Remote Source :interrobang:

For accessing the Cassandra on a remote server, you should define the `host` and `port` attributes of the connector. Like the past, also it can be done on two manner: running flag and session building time configurations.

### Running flag

With putting `conf` on the running command, you could change the configurations of the process. For our purpose, we can do like this:

```bash
--conf spark.cassandra.connection.host=xxx.xxx.xxx.xxx --conf spark.cassandra.connection.port=yyyyy
```

sol we should have something like this for example:

```bash
pyspark --packages com.datastax.spark:spark-cassandra-connector_2.11:2.3.2 --conf spark.cassandra.connection.host=xxx.xxx.xxx.xxx --conf spark.cassandra.connection.port=yyyyy
```

:warning: The `conf` flag, always **MUST BE** after the `packages` flag.

### Session Building Time

On creation of spark session, we can set the `host` and `port` attribute of the connector package. For example we have:

```R
config$spark.cassandra.connection.host = "xxx.xxx.xxx.xxx"
config$spark.cassandra.connection.port = "yyyyy"
```

so we should have something like this:

```R
library(sparklyr)
library(crassy)
library(SparkR)

config <- spark_config()

config$sparklyr.defaultPackages = "com.datastax.spark:spark-cassandra-connector_2.11:2.3.2"

config$spark.cassandra.connection.host = "xxx.xxx.xxx.xxx"
config$spark.cassandra.connection.port = "yyyyy"

config$sparklyr.gateway.port = 10000
config$sparklyr.gateway.connect.timeout = 1
config$sparklyr.gateway.start.wait = 1000

sc <- spark_connect(master='local', spark_home='SPARK_HOME', config=config)

spk_handle = spark_load_cassandra_table(sc=sc, cass_keyspace="KEYSPACE", cass_tbl="TABLENAME", spk_tbl_name="SPARKTABLE")
```

