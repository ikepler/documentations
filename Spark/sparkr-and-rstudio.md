# Spark and RStudio

For using Spark inside the RStudio, you should install `sparklyr`, `SparkR` and `ikeplers/crassy` packages. The last package is a fork from [AkhilGNair/crassy](https://github.com/AkhilGNair/crassy)  which has been abandoned and now will be maintained from *iKepler* team and should be installed with `devtools` library.

After that you can connect to spark in this manner:

```R
library(sparklyr)
library(crassy)
library(SparkR)

config <- spark_config()

config$sparklyr.gateway.port = 10000
config$sparklyr.gateway.connect.timeout = 1
config$sparklyr.gateway.start.wait = 1000

sc <- spark_connect(master='local', spark_home='SPARK_DIRECTORY', config=config)
```

You have to fill `spark_home` argument with proper location of your Spark installation directory (e.g. `/opt/spark` or something like that). `sc` now is your `SparkSession`! 