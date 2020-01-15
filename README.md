---
# Related publishing issue: https://github.ibm.com/IBMCode/Code-Tutorials/issues/2677

authors:
  - email: "Emre.Kutlug@ibm.com"
    name: "Emre Kutlug"
components:
  - "jupyter"
  - "watson-studio"
runtimes:
  - "python-runtime"
services:
  - "apache-spark"
  - "python"
  - "watson-studio"
tags:
  - "data-science"
  - "machine-learning"
abstract: "This tutorial covers Big Data via PySpark (a Python package for spark programming). We explain SparkContext by using map and filter methods with Lambda functions in Python. We also create RDD from object and external files, transformations and actions on RDD and pairRDD, SparkSession, and PySpark DataFrame from RDD, and external files. In addition, we use sql queries with DataFrames (by using Spark SQL module). And finally, machine learning with PySpark MLlib library."
completed_date: "2020-01-10"
draft: true
excerpt: "This tutorial covers Big Data via PySpark (a Python package for spark programming). We explain SparkContext by using map and filter methods with Lambda functions in Python. We also create RDD from object and external files, transformations and actions on RDD and pair RDD, SparkSession, and PySpark DataFrame from RDD, and external files. In addition, we use sql queries with DataFrames (by using Spark SQL module). And finally, machine learning with PySpark MLlib library."
last_updated: "2020-01-10"
meta_description: "This tutorial covers Big Data via PySpark (a Python package for spark programming). We explain SparkContext by using map and filter methods with Lambda functions in Python. We also create RDD from object and external files, transformations and actions on RDD and pair RDD, SparkSession, and PySpark DataFrame from RDD, and external files. In addition, we use sql queries with DataFrames (by using Spark SQL module). And finally, machine learning with PySpark MLlib library."
title: "Getting started with PySpark"
subtitle: "Learn to use PySpark for processing structured data and machine learning modeling"
meta_title: "Getting started with PySpark"
primary_tag: analytics
type: tutorial
ignore_prod: false
---

Apache Spark is a fast and powerful framework that provides an API to perform massive distributed processing over resilient sets of data. The main abstraction Spark provides is a resilient distributed dataset (RDD), which is the fundamental and backbone data type of this engine. Spark SQL is Apache Spark's module for working with structured data and MLlib is Apache Spark's scalable machine learning library. Apache Spark is written in Scala programming language. To support Python with Spark, the Apache Spark community released a tool, PySpark. PySpark has similar computation speed and power as Scala. PySpark is a parallel and distributed engine for running big data applications. Using PySpark, you can work with RDDs in Python programming language.

This tutorial explains how to set up and run Jupyter Notebooks from within IBM® Watson™ Studio. We will use two different datasets 5000_points.txt and people.csv that are available on [github](https://github.com/emrekutlug/Getting-started-with-PySpark/tree/master/datasets). The data set has a corresponding [Getting Started with PySpark Notebook](https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/getting_started_with_pyspark.ipynb).


## Learning objectives

In this tutorial, you will learn:

1. Big Data analysis with PySpark
2. Using sql queries with Dataframes by using Spark SQL module
3. Machine learning with MLlib library

## Prerequisites

To complete the tutorial, you need an [IBM Cloud account](https://cloud.ibm.com/registration). You can obtain a free trial account, which gives you access to [IBM Cloud](https://cloud.ibm.com/login) and [IBM Watson Studio](https://www.ibm.com/cloud/watson-studio).

## Estimated time
It should take you approximately 60 minutes to complete this tutorial.

## Steps

### Create IBM Cloud Object Storage service

An Object Storage service is required to create projects in Watson Studio. If you do not already have a storage service provisioned, complete the following steps:

1. From your IBM Cloud account, search for “object storage” in the IBM Cloud Catalog. Then, click the **Object Storage** tile.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2014.43.04.png" alt="drawing" width="800" height="400"/>

2. Choose Lite plan and Click **Create** button.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2014.46.54.png" alt="drawing" width="800" height="400"/>

### Create Watson Studio service

1. From your IBM Cloud account, search for “watson studio” in the IBM Cloud Catalog. Then, click the Watson Studio tile.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2014.49.52.png" alt="drawing" width="800" height="400"/>

2. Choose Lite plan and Click **Create** button.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2014.50.57.png" alt="drawing" width="800" height="400"/>

### Create Watson Studio project

1. Click **Get Started**.

2. Click either **Create a project** or **New project**.

3. Select **Create an empty project**.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2014.55.39.png" alt="drawing" width="800" height="400"/>

4. In the New project window, name the project (for example, “Getting Started with PySpark”).

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2014.58.48.png" alt="drawing" width="800" height="400"/>

5. For Storage, you should select the IBM Cloud Object Storage service you created in the previous step. If it is the only storage service that you have provisioned, it is assigned automatically.

6. Click Create.

### Upload data set

Next, you’ll download the data set from Github and upload it to Watson Studio.

1. Navigate to the URL for the data set on Github (https://github.com/emrekutlug/Getting-started-with-PySpark/tree/master/datasets), and download the file to your local desktop.

2. In Watson Studio, select **Assets**.

3. If not already open, click the **1001** data icon at the upper right of the panel to open the **Files** sub-panel. Then, click **Load**.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2015.08.27.png" alt="drawing" width="800" height="400"/>

4. Drag the files to the drop area or **browse** for files to upload the data into Watson Studio.

5. Wait until the file has been uploaded.

### Create the notebook

Create a Jupyter Notebook and change it to use the data set that you have uploaded to the project.

1. In the **Asset** tab, click **Add to Project**.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2015.12.28.png" alt="drawing" width="800" height="400"/>

2. Select the **Notebook** asset type.

3. On the New Notebook page, configure the notebook as follows:

    1. Select the **From URL** tab:
    
    
    <img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2016.23.57.png" alt="drawing" width="800" height="400"/>
    
    2. Enter the name for the notebook (for example, ‘getting-started-with-pyspark’).

    3. Select the Spark Python 3.6 runtime system.

    4. Enter the following URL for the notebook:
    
    ```python
    https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/getting_started_with_pyspark.ipynb
    ```
    5. Click Create Notebook. This initiates the loading and running of the notebook within IBM Watson Studio.
    
### Run the notebook

The notebook page should be displayed.

If the notebook is not currently open, you can start it by clicking the Edit icon displayed next to the notebook in the Asset page for the project:

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-23%20at%2016.28.51.png" alt="drawing" width="800" height="400"/>
    

### What is SparkContext?

Spark comes with an interactive python shell that has PySpark already installed. PySpark automatically creates a SparkContext for you in the PySpark Shell. SparkContext is an entry point into the world of Spark. An entry point is a way of connecting to Spark cluster. We can use SparkContext using sc variable. In the following examples, we retrieve SparkContext version and Python version of SparkContext.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2009.57.11.png" alt="drawing" width="800" height="200"/>

### Using map and filter methods with Lambda function in Python

Lambda functions are anonymous functions in Python. Anonymous functions do not bind to any name in runtime and it returns the functions without any name. They are usually used with map and filter methods. Lambda functions create functions to be called later. In the following example, we use lambda function with map and flter methods.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2009.58.22.png" alt="drawing" width="800" height="150"/>

### Creating RDD from Object

RDDs are data stacks distributed throughout a cluster of computers. Each stack is calculated on different computers in the cluster. RDDs are the most basic data structure of Spark. We can create RDDs by giving existing objects like Python lists to SparkContext's parallelize method. In the following example, we create a list with numbers and create a RDD from this list.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2009.59.33.png" alt="drawing" width="800" height="150"/>

### Transformations and Actions on RDD

Transformations and actions are two type of operations in Spark. Transformations create new RDDs. Actions performs computation on the RDDs. Map, filter, flatmap and union are basic RDD transformations. Collect, take, first and count are basic RDD actions. In the following example, we create rdd named numRDD from list and then using map transformation we create a new rdd named cubeRDD from numRDD. Finally, we use collect action to return a list that contains all of the elements in this RDD.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.00.58.png" alt="drawing" width="800" height="200"/>

### Transformations and Actions on pair RDD

Pair RDD is a special type of RDD to work with datasets with key/value pairs. All regular transformations work on pair RDD. In the following example, we create pair RDD with 4 tuple with two numbers. In each tuple, the first number is key and the second number is value. Then, we apply reduceByKey transformation to pair RDD. ReduceByKey transformation combine values with the same key. Therefore, this transformation adds the values of tuples with the same key.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.01.55.png" alt="drawing" width="800" height="200"/>

We can sort keys of tuples using sortByKey transformation like in the following example.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.03.27.png" alt="drawing" width="800" height="150"/>

We can count the number of tuples with the same key. In the following example, we see (3,2) because there are two tuple with key 3 in pair RDD.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.05.10.png" alt="drawing" width="800" height="200"/>

### What is SparkSession?

SparkContext is the main entry point for creating RDDs while SparkSession provides a single point of entry to interact with Spark Dataframes. SparkSession is used to create DataFrame, register DataFrames, execute SQL queries. We can access SparkSession in PySpark using spark variable. In the following examples, we retrieve SparkSession version and other informations about it.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.06.25.png" alt="drawing" width="800" height="150"/>

### Creating PySpark DataFrame from RDD

Spark SQL which is a Spark module for structured data processing provides a programming abstraction called DataFrames and can also act as a distributed SQL query engine. In the following example, we create rdd from list then we create PySpark dataframe using SparkSession's createDataFrame method. When we look at the type of dataframe, we can see pyspark.sql.dataframe as an output. Furthermore, we can use show method to print out the dataframe.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.08.10.png" alt="drawing" width="800" height="300"/>


### Add Datasets

We can use external datasets in notebook to do this select the cell below. If not already open, click the **1001** data icon at the upper part of the page to open the Files subpanel. In the right part of the page, select the people.csv dataset. Click insert to code, and click Insert SparkSession DataFrame.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.16.10.png" alt="drawing" width="800" height="400"/>

You can delete df_data_1.take(5) part and then copy cos.url('file_name', 'bucket_name') above it then assign cos.url('file_name', 'bucket_name') to path_people variable and comment out this variable. cos.url('file_name', 'bucket_name') is path to your file you can access the file by using this path.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.50.49.png" alt="drawing" width="800" height="300"/>

You can also add 5000_points.txt dataset by applying same procedure but click insert to code then click insert credentials then write "file" and "bucket" values inside "path_5000 = cos.url('file_name', 'bucket_name')" expression and comment out path_5000.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.52.52.png" alt="drawing" width="800" height="200"/>

### Create PySpark DataFrame from external file

We can create PySpark DataFrame by using SparkSession's read.csv method. To do this, we should give path of csv file as an argument to the method. Show action prints first 20 rows of DataFrame. Count action prints number of rows in DataFrame. Columns attribute prints the list of columns in DataFrame. PrintSchema action prints the types of columns in the DataFrame and tells you if there are null values in columns.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.54.13.png" alt="drawing" width="800" height="400"/>

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.55.17.png" alt="drawing" width="800" height="300"/>

We can use select method to select some columns of DataFrame. If we give an argument to show method, it prints out rows as the number of arguments. In the following example, it prints out 10 rows. dropDuplicates method removes the duplicate rows of a DataFrame. We can use count action to see how many rows are dropped.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.56.39.png" alt="drawing" width="800" height="300"/>

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.57.43.png" alt="drawing" width="800" height="150"/>

We can filter out the rows based on a condition by using filter transformation as in the following example.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2010.59.08.png" alt="drawing" width="800" height="300"/>

We can group columns based on their values by using groupby transformation as in the following example.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2011.07.00.png" alt="drawing" width="800" height="400"/>

We can rename a column in DataFrame by using withColumnRenamed transformation.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2011.07.35.png" alt="drawing" width="800" height="200"/>

### Use SQL queries with DataFrames by using Spark SQL module

We can also use SQL queries to achieve the same things with DataFrames. Firstly, we should create temporary table by using createOrReplaceTempView method. We should give the name of temporary table as an argument to the method. Then, we can give any query we want to execute to SparkSession's sql method as an argument. Look at the following example.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2011.08.20.png" alt="drawing" width="800" height="300"/>

### Create RDD from external file

The second and most common way to create RDDs is from an external data set. To do this, we can use SparkContext's textFile method. In the following example, we use 5000_points.txt dataset. To do this, we use path to dataset as an argument to textFile method.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2011.09.36.png" alt="drawing" width="800" height="200"/>

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2011.10.57.png" alt="drawing" width="800" height="300"/>

We can also further transform the splitted RDD to create a list of integers for the two columns.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2011.12.24.png" alt="drawing" width="800" height="200"/>

### Machine Learning with PySpark MLlib

PySpark MLlib is the Apache Spark's scalable machine learning library in Python consisting of common learning algorithms and utilities. We use K-means algorithm of MLlib library to cluster data in 5000_points.txt dataset. First, we should define error method to calculate distance from every point to center of its clusters which the points belong to.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2011.41.34.png" alt="drawing" width="800" height="75"/>

We train the model with 4 different number of clusters from 13 to 16 and then calculate the error for all of them. As you see in the output, 16 clusters give minimum error. We retrain the model with the number of cluster with the smallest error. We then use clusterCenters attribute to see the center of all clusters.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2011.44.41.png" alt="drawing" width="800" height="400"/>

We can again use SparkSession's createDataFrame method to create DataFrame from rdd. We must convert PySpark DataFrame to Pandas DataFrame in order to visualise data. To do this, we can use toPandas method. We create another Pandas DataFrame from cluster centers list. Then, using matplotlib's scatter method, we can make plot for clusters and their centers.

<img src="https://github.com/emrekutlug/Getting-started-with-PySpark/blob/master/screenshots/Screen%20Shot%202019-12-24%20at%2011.45.38.png" alt="drawing" width="800" height="400"/>

## Summary

This tutorial covered Big Data via PySpark (a Python package for spark programming). We explained SparkContext by using map and filter methods with Lambda functions in Python. We also created RDD from object and external files, transformations and actions on RDD and pair RDD, SparkSession, and PySpark DataFrame from RDD, and external files. Next, we used sql queries with DataFrames (by using Spark SQL module). And finally, machine learning with PySpark MLlib library.


