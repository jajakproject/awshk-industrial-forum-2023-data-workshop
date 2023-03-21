# Overview
**Amazon Athena**: Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. You can quickly query your data without having to setup and manage any servers or data warehouses. Amazon Athena automatically executes queries in parallel, so most results come back within seconds. Athena is out-of-the-box integrated with AWS Glue Data Catalog, allowing you to create a unified metadata repository across various services, crawl data sources to discover schemas and populate your Catalog with new and modified table and partition definitions, and maintain schema versioning. Amazon Athena uses Presto with ANSI SQL support and works with a variety of standard data formats, including CSV, JSON, ORC, Avro, and Parquet. Amazon Athena uses Amazon S3 as its underlying data store, making your data highly available and durable.

## Setup Athena
1. Open the **Amazon Athena console** 

2. Click the **Launch query editor** button in the top-right corner.

3. Click on the **Settings** tab and then **Manage** in the top right corner to set the Query result location and encryption by clicking the link and providing an Amazon S3 bucket location to be used for your Athena results. (e.g. s3://awshk-industrial-forum-2023-{aws-account-number}/athena-results/)

4. Click **Save**.

5. Back to **Editor** tab, Data source select `AwsDataCatalog`, Database select `ecommerce-data`.

6. Try running the following query in the query editor
```SQL
SELECT * FROM "ecommerce-data"."mytable" where Month = 'Feb';
```

