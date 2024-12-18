# AWSGlueExample

General AWS Glue Concept

Note: referring to the AWS Glue Concept diagram

AWS Glue Datacatalog sits at the CENTRE of everything AWS Glue

it is a Persistent Metadata Store
it retains information such as 

i) Schema
ii) Data location
iii) Data types
iv) Data Classification

the referred Database and tables are information ABOUT the data, where the actual data will still reside where it has been.

![image](https://github.com/user-attachments/assets/7671e20c-39dc-41bf-a5a8-c1bcd86338aa)

Project Steps:
1) Create S3 buckets for data source and targets with the following folder structure. These Partitions make querying the data more efficently


``` mermaid
graph TD;
      A[Buckets] --> B[aws-glue-pract-tks]
      B --> C[data]
      C --> D[customer_database]
      D --> E[customer_csv - source]
      E --> F[dataload=17122024]
      B --> G[Scripts]
      B --> H[temp_dir]
      B --> I[athena_results]
      D --> J[customer_parquet - target]
      F --> K[.csv data file]
      J --> L[parquet datafile]

```

2) create AWS service role for Glue, include permission to access s3
3) load the csv file found in this repo
4) create the database on Glue
5) Create Crawler to bring the schema information across to the glue datacatalog, the data itself will sit and remain where it lives.
6) 
