# Big-Data

## Background

Amazon's shoppers depend on product reviews to make a purchase. Amazon makes these datasets publicly available. They are quite large and can exceed the capacity of local machines. One dataset alone contains over 1.5 million rows; with over 40 datasets, data analysis can be very demanding on the average local computer. The goal is be to perform the ETL process completely in the cloud and upload a DataFrame to an RDS instance. 

This homework assignment contains two levels. The second level is optional but highly recommended.

1. Create DataFrames to match production-ready tables from two big Amazon customer review datasets.

2. Analyze whether reviews from Amazon's Vine program are trustworthy.

- - -

## Instructions

### Level 1

* Use the provided schema to create tables in your RDS database.

* Create two separate Google Colab notebooks and **extract** any two datasets from the list at [review dataset](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt). Put each dataset into its own notebook.

  **Note:** You could ETL both data sources in a single Colab notebook, but it will be easier to work with these large S3 data sources in separate notebooks.

* Be sure to handle the header correctly. If you read the file without the header parameter, you may find that the column headers are included in the table rows.

* Complete the following steps for each notebook (one dataset per notebook).

  * Count the number of records (rows) in the dataset.

  * Transform the dataset to fit the tables in the [schema file](../Resources/schema.sql). Be sure that the DataFrames match in data type and in column name.

  * Load the DataFrames that correspond to tables into an RDS instance. **Note:** This process can take up to 10 minutes for each. Ensure that everything is correct before uploading.
  
  # First Data - One 
![image](https://user-images.githubusercontent.com/99145651/186796767-677eb045-5a31-44b8-8099-b7280cfb02ff.png)

![image](https://user-images.githubusercontent.com/99145651/186796864-91338b85-8a7e-4c5b-8da6-53979a5c1fb9.png)

![image](https://user-images.githubusercontent.com/99145651/186796936-604e55ee-7a57-48fe-b34c-d83fab65d3fd.png)

![image](https://user-images.githubusercontent.com/99145651/186796999-232f0d56-769c-4963-82c1-6cf05b6db5a9.png)

![image](https://user-images.githubusercontent.com/99145651/186797077-1e21e54f-d78b-4e92-9b4e-09b200b208c2.png)

  # Second Data - Two 

![image](https://user-images.githubusercontent.com/99145651/187036508-828befb0-a698-4c89-acad-d86edf7c6fba.png)

![image](https://user-images.githubusercontent.com/99145651/187036701-fa93ef93-3f8c-4f61-8ad0-903c644c3772.png)

![image](https://user-images.githubusercontent.com/99145651/187036728-85050634-9104-4576-b292-dd3404ad5339.png)

![image](https://user-images.githubusercontent.com/99145651/187036752-a6e598b7-44e5-4fdb-8af9-5fb7214a0630.png)

![image](https://user-images.githubusercontent.com/99145651/187036776-505cfede-ae4c-44a8-994b-964ef5d823e9.png)


### Level 2

In Amazon's Vine program, reviewers receive free products in exchange for reviews.

 ![image](https://user-images.githubusercontent.com/99145651/187041902-cba8dd7c-ef24-4c38-855d-0232de63fcea.png)

Amazon has several policies to reduce the bias of its Vine reviews: [https://www.amazon.com/gp/vine/help?ie=UTF8](https://www.amazon.com/gp/vine/help?ie=UTF8).

But are Vine reviews truly trustworthy? Investigate whether Vine reviews are free of bias. Use either PySpark or, for an extra challenge, SQL to analyze the data.

* With SQL, first use Spark on Colab to extract and transform the data and then load it into a SQL table on your RDS account. Perform analysis with SQL queries on RDS.

* Consider steps such as filtering for reviews that meet a certain number of helpful votes, total votes, or both.

* Submit a summary of your findings and analysis.

![image](https://user-images.githubusercontent.com/99145651/187281060-c5bdff85-adf8-4d75-abbe-3f23212fa874.png)

![image](https://user-images.githubusercontent.com/99145651/187281169-d3cc705a-fe7d-4911-928c-f0f05299e988.png)

Based on review of the above results, I would concluded the that reviews are slightly bias. Approxiametly, 51% of paid reviwers provide a 5 star review.
However, there are a small number of reviewers being paid. (142). As opposed to 40471 with just under 39% providing a 5 star review.
- - -

## Hints and Considerations

* Start each notebook with the following code in the first cell, and be sure to update the Spark version.

```python
import os
# Find the latest version of spark 3.0  from http://www-us.apache.org/dist/spark/ and enter as the spark version
# For example:
# spark_version = 'spark-3.0.1'
spark_version = 'spark-3.<spark version>'
os.environ['SPARK_VERSION']=spark_version

# Install Spark and Java
!apt-get update
!apt-get install openjdk-11-jdk-headless -qq > /dev/null
!wget -q http://www-us.apache.org/dist/spark/$SPARK_VERSION/$SPARK_VERSION-bin-hadoop2.7.tgz
!tar xf $SPARK_VERSION-bin-hadoop2.7.tgz
!pip install -q findspark

# Set Environment Variables
import os
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-11-openjdk-amd64"
os.environ["SPARK_HOME"] = f"/content/{spark_version}-bin-hadoop2.7"

# Start a SparkSession
import findspark
findspark.init()
```
![image](https://user-images.githubusercontent.com/99145651/187036922-95622468-82bd-412e-9012-c96ad63820fc.png)


* For connection to Postgres, run the following code in the next cell.

```python
!wget https://jdbc.postgresql.org/download/postgresql-42.2.9.jar
```
![image](https://user-images.githubusercontent.com/99145651/187037003-dd6d6854-14ed-4115-95ba-49f7a8cc04d0.png)

- - -


## References

Amazon customer Reviews Dataset. (n.d.). Retrieved April 08, 2021, from: [https://s3.amazonaws.com/amazon-reviews-pds/readme.html](https://s3.amazonaws.com/amazon-reviews-pds/readme.html)

---




