# Lending-Club-Data-Analysis-using-PySpark

**Step1:**  Create cluster and load the dataset into the databricks.

**Step2:** Read the csv file using spark.read.format and display using `display()` command.

**Step3:** Check the number of rows: `df.count()`

**Step4:** Print out the schema in the tree format: `df.printSchema()` Optionally allows to specify how many levels to print if schema is nested. <br />
      - Here we can see some columns such as term, emp_length are identified as string which needs cleanup.

**Step5:** Creates or replaces a local temporary view of df: df.createOrReplaceTempView(). By creating a temp view we can work with this data using SQL. By doing this, we can manipulate the data using SQL queries. If we want to use a different language other than Python, we need to use the % magic command before the language name, as Python is the default language for this notebook.

**Step6:** To check the descriptive stats of the given dataset: `df.describe().show()`. We do not get a definite output for this, since the dataset needs cleanup.

**Step7:** Select only the columns that are needed for this analysis: `df.select()`. Even then we cannot see the stats properly.

**Step8:** So we are using `df_selected.cache()` where .cache() method is used to persist a DataFrame or RDD in memory. When you cache a DataFrame or RDD, it is stored in memory the first time it is computed, which allows subsequent actions on the same data to be much faster. This is especially useful when you have multiple actions that need to be performed on the same DataFrame or RDD. <br />
      - Like most operations in Spark, caching is lazy. The DataFrame/RDD is not actually cached until an action (such as count(), collect(), or show()) is performed on it. <br />

      So what is RDD?<br />
      RDD stands for Resilient Distributed Dataset. It is a fundamental data structure of Apache Spark, representing an immutable distributed collection of objects that can be processed in parallel. Here are the key features and concepts related to RDDs: <br />
      1. Immutable<br />
      2. Distributed<br />
      3. Fault tolerance<br />
      4.Lazy Evaluation<br />

**Step8:** Now we use `show()` with `.describe()` which much more limited columns and we get a output that is interpretable. From the output we can see that the columns "emp_length" and "revol_util" are null since they are treated as string data types. Additionally, the mean, standard deviation, and maximum values of the "dti" column indicate the presence of a potential outlier.

**Step8:** Cleanup "emp_length" column using regexp_replace(), regexp_extract(), col() functions from `pyspark.sql.functions`
