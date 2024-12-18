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
5) Create Crawler to bring the schema information across to the glue datacatalog, the data itself will sit and remain where it lives. (instead of creating the schema manually)
      - you will also need to specify the partition column name - in this example it's called Dataload
      - also specify the type of the data, int, bool etc
   - then you can run the crawler with the source being the customer csv (original data) and the output to the AWS Glue database (where the schema will live, not the actual data)
   - then the table will be added once you run the crawler
   
6) before you run any ETL job, you can view the data using Athena, just need to make sure there is an s3 place for the athena results
7) now we can define our ETL Job!
      In this example we just want to transform the csv into parquet format and remove any nulls

8) The visual editor was used to add 3 blocks, by selecting the source, transform and target tabs of the visual editor

![image](https://github.com/user-attachments/assets/d6bafad9-bf8f-4913-926a-52980a5e5400)

9) Now, navigate to the Trigger tab to build some trigger events, where you can set up a trigger of another job on completion of the first job, or set a schedule or even a cron expression
