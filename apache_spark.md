## Introduction to Spark (Beginner's guide to Spark and PySpark):

As a beginner, I was taught to use Python which is most likely for everybody else. With that, I got hooked onto python and it's various libraries or rather started using python libraries instead of shifting to another language. I use *numpy, scipy* and *Scikit-Learn* for basic ML algorithms and *Keras* framework with backend *theano*. My major interests lie in Neural Networks and NLP, essentially as of now towards the implementation and practical applications but I want to extend further into theory behind.

I had absolutely no clue about Spark as I start this blog. I am going to put all resources and my learning process documented in this.

So I am huge fan of Pandas, I use it everyday to manipulate data and it gets my work done because I have some MB of data each time. I heard about Spark DataFrame analogous to Pandas DataFrame with better optimizations under the hood and I wanted to give it a shot.

So Spark saves data as **Resilient Distributed Dataset (RDD)**.

- Resilient - when Dataset crashes, Spark can fetch and continue the processes for you as they are fault tolerant
RDDs are immutable, we cannot delete data but we can apply transformations and save it again
- Distributed - RDDs do not contain data, they just contain references to the data.
- Dataset - they can contain any type of data from any language like Scala, R, Python and so on.

## Apache Spark Components:
1. Drivers
2. Workers
3. Executors
4. Cluster Managers

### 1. Drivers:
Driver Node converts user program into tasks and sends into worker nodes. which are computed by worker nodes.
### 2. Workers:
These are compute nodes where execution takes place.
### 3. Executors:
These are the JVM processes within nodes, they run the application. They provide in-memory that are cached by RDDs.
### 4. Cluster Manager:
It is external service which launches application oSpark contains a default manager namely Standalone cluster manager. Some external cluster managers are Apache Mesos and Hadoop YARN.

### Architecture during run-time:
The driver node converts the user program into transformations and actions. This is converted into Directed Acyclic Graph (DAG). It also performs optimization at this stage like pipeline changes and converts logical graph into physical execution plan. Then it creates tasks which are bundled to be send to cluster. Now driver talks to cluster manager and creates worker nodes on behalf of the driver. Now when execution starts in worker nodes and driver program will monitor the set of executors which run. User program might cache data based on the program and the driver tracks the location of cached data to schedule future tasks.

![Run-time Architecture](https://github.com/HimaVarsha94/Spark-for-beginners-with-Python-/blob/master/run_time_spark.png)
### Reasons I think Spark DataFrame is awesome:
##### DataFrame:
It is a distributed collection of data into columns similar to Pandas. It being similar to Pandas helps as one can use similar or same syntax.
```
# Create a new DataFrame that contains “young users” only
young = users.filter(users.age < 21)
# Alternatively, using Pandas-like syntax
young = users[users.age < 21]
# Increment everybody’s age by 1
young.select(young.name, young.age + 1)
# Count the number of young users by gender
young.groupBy(“gender”).count()
```
### Spark sql
I think the coolest part is inclusion of sql using spark sql. For instance,
```
context.sql(“SELECT count(*) FROM young”)
```
### Conversion into Pandas DataFrame
To add more, you can convert to and fro from Spark DataFrame to Pandas DataFrame.

### Supported Data Formats

With such petabytes of data out there, I think different companies or people prefer different data formats to save data. Spark supports reading data from most formats like JSON, Hive tables etc.

### Conclusion:
I think Pandas is easier to use and for users who are already proficient, they should utilise it. If data cannot be handled using Pandas, Spark is amazing.
### Framework:
I surfed and found PySpark - Python API for Spark. Spark is a distributed computing framework, according to the technical jargon. I like to put it in a simpler way, one guy eating a pizza will take more time than six eating the pizza. But at the same time, if 2 guys have to eat the same slice of pizza, it might not be easy and efficient. Similarly, I will cite examples where we can employ Spark and where there is no effect.

PySpark helps data scientists interface with Resilient Distributed Datasets (RDD) in apache spark and python.

Follow this [useful guide](https://github.com/HimaVarsha94/Spark-for-beginners-with-Python-/blob/master/PySpark installation guide for MacOS users.md) for installation of PySpark on Mac Systems. This is for ubuntu users but since I use iOS environment, I made changes accordingly and you can find the complete information here.

In Spark, there is a master node and worker nodes. The master nodes gives instructions to the worker nodes which contain executors.
#### Lazy execution of Spark:
Spark implements only when needed. It means that assume we say:
```
from pyspark import SparkContext
sc = SparkContext()
sc.parallelize(range(0,10))
```
This doesn't do much, but when we do this:
```
sc.parallelize(range(0,10)).first()
```
Now, it creates a spark context and returns the first value which is 0.

References:
1. https://www.youtube.com/watch?v=m4pYYnY4_gU
2. Databricks blogs
