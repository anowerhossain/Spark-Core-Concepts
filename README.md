## Apache Spark Core Concepts 🌟
Apache Spark is an open-source, distributed computing system that enables fast, large-scale data processing.

### RDD (Resilient Distributed Dataset) 📊
RDD is the fundamental data structure in Spark. It represents a distributed collection of objects that can be processed in parallel across the cluster.
-- Immutable
-- Distributed
-- Fault-tolerant

### DataFrame 🗂️
DataFrame is a distributed collection of data organized into named columns (like a table in SQL). It supports a variety of operations and is optimized for performance.
-- Built on top of RDDs
-- Supports querying through SQL or DataFrame API.
-- Optimized execution plans through Catalyst Optimizer.

### SparkContext & SparkSession 🚀

-- SparkContext: The entry point to Spark functionality. It's responsible for connecting to the cluster and creating RDDs.
-- SparkSession: A unified interface for working with DataFrames, SQL, and RDDs. It is the new entry point introduced in Spark 2.x

### Cluster Manager 🖧
The cluster manager manages the resources and schedules tasks on the cluster. Spark can run on various cluster managers: YARN (Hadoop). 

### DAG (Directed Acyclic Graph) 🔗
Spark creates a DAG of stages for all the operations to be performed. This structure allows Spark to execute tasks in parallel while managing dependencies.

-- Provides fault tolerance.
-- Enables optimization through task pipelining.

### Transformations & Actions 🔄⚡
-- Transformations: Operations that create a new RDD/DataFrame from an existing one (e.g., map(), filter()). They are not executed immediately, but only when an action is called and it refers to Lazy Evaluation. 
-- Actions: Operations that trigger execution (e.g., collect(), count(), save()). Actions cause Spark to execute the transformations. 

### Caching and Persistence 💾
-- Caching: Spark allows you to cache or persist an RDD/DataFrame to memory to speed up future computations.
-- Use Cases: Use caching when you need to perform multiple actions on the same dataset.

### Setting Up SparkSession and Loading Data 📂
```pyhton
from pyspark.sql import SparkSession

# Initialize Spark session
spark = SparkSession.builder.appName("SparkCoreConcepts").getOrCreate()

# Load data into DataFrame (Example: CSV file)
df = spark.read.csv("example_data.csv", header=True, inferSchema=True)

# Show the top 5 rows of the DataFrame
df.show(5)
```

### RDD Example: Transformations and Actions 🔄⚡
```python
# Convert DataFrame to RDD
rdd = df.rdd

# Transformation: map() - Multiply values of a specific column by 2
rdd_transformed = rdd.map(lambda x: (x[0], x[1] * 2))  # Assuming x[0] is name, x[1] is a numeric value

# Action: collect() - Collect the results to the driver program
result = rdd_transformed.collect()

# Print the results
print(result)
```

### DataFrame Example: SQL Queries 🗂️
```python
# Register DataFrame as a temporary SQL table
df.createOrReplaceTempView("data_table")

# Run SQL query to filter data
filtered_df = spark.sql("SELECT * FROM data_table WHERE column_name > 1000")

# Show filtered results
filtered_df.show()
```

### Writing Data to a File (Action) 💾
```python
# Writing the DataFrame to a CSV file
filtered_df.write.csv("output_data.csv", header=True)
```




