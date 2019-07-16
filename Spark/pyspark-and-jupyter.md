# PySpark and Jupyter

For using PySpark as the python kernel provider in Jupyter, you should change its runtime driver parameters. For do this, you should define this enviromental variables inside your shell:

```bash
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS=notebook
```

now run `pyspark` and all is done :wink:.