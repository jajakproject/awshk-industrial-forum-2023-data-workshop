# Overview
Querying on raw data is usually not optimized due to missing partition and compression. Even worse, the data format is not columnarized where query or analytic is not feasible. ETL Operations are required in order to optimize data analytic.

In this lab, you will create an AWS Glue transform job via Glue Studio  to perform basic transformations on your S3 source data. Specifically, we will:

- Convert raw CSV in s3://awshk-industrial-forum-2023-{aws-account-number}/mytable/* to a compressed columnar format (Apache Parquet)
- Partition data by Month

**ETL Operations**: using the metadata in the Data Catalog, AWS Glue can auto-generate Scala or PySpark scripts with AWS Glue extensions that you can use and modify to perform various ETL operations. For example, you can extract, clean, and transform raw data, and then store the result in a different repository, where it can be queried and analyzed. Such a script might convert a CSV file into a relational form and save it in Amazon Redshift. AWS Glue runs your ETL jobs in an Apache Spark  serverless environment.

**ETL Jobs**: the AWS Glue Jobs system provides managed infrastructure to orchestrate your ETL workflow. Jobs can be scheduled and chained, or they can be triggered by events such as the arrival of new data. You can run your job on demand, or you can set it up to start when a specified trigger occurs. The trigger can be a time-based schedule or an event. Glue Studio provides a comprehensive job monitoring dashboard to get a global view of your ETL jobs (e.g. Execution details, resource usage etc.)

## Setup ETL Job
1. Proceed to the AWS Glue Studio console 
2. Click View Jobs to create a new job.
- Under **Create Job** section, choose **Visual with a source and target** and select **Amazon S3** from dropdown for both **Source** and **Target**.
- Click **Create** button.
<img width="1044" alt="image" src="https://user-images.githubusercontent.com/108851851/226196353-f47497de-5379-42b2-b96a-7c8ae6a71bef.png">

3. On the next screen you’ll see Visual representation of transformation we’re going to apply. Switch to Job details tab and fill in the following:
- Name: `transform-csv-to-parquet`
- IAM Role: Select `AWSGlueServiceRole-industrialforum`
- Glue version: `Glue 3.0 - Supports spark 3.1, Scala 2, Python 3`
- Language: `Python 3`
- Worker type: `G 1X`

4. Now switch to “Visual” tab to configure Source & targets of our transformation
- Click on top node in editor Data Source - S3 bucket and on the right switch to tab Data source properties - S3:
  - S3 source type choose `Data Catalog table`
  - Choose Database you created in previous lab: e.g. ecommerce-data
  - Table: mytable
<img width="948" alt="image" src="https://user-images.githubusercontent.com/108851851/226196982-95b7cfe9-4573-45be-88a3-39b2a2a93d57.png">

- Click on target node at the bottom: **Data target - S3 bucket** and configure the following.
  - In Format: Parquet
  - Compression type: Snappy
  - Then click Browse S3 and choose our datalake bucket as the target S3 bucket for the Parquet files this job will produce.
  - Then in the field S3 location target add mytable-parquet/ to bucket name, so it looks like s3://awshk-industrial-forum-2023-{aws-account-number}/mytable-parquet/
  - Then in Data Catalog update options, select **Create a table in the Data Catalog and on subsequent runs, update the schema and add new partitions**
  - Then in Database, select `ecommerce-data`
  - Then in Table name, input `mytable-parquet`
  - Lastly, click **Add a partition key**, select `Month`
  <img width="964" alt="image" src="https://user-images.githubusercontent.com/108851851/226197408-b2ce1dd2-988d-40f5-b099-9e1153b820ae.png">
<img width="456" alt="image" src="https://user-images.githubusercontent.com/108851851/226197532-fd744409-2768-4156-9ccf-e22cc9e7eb17.png">
<img width="457" alt="image" src="https://user-images.githubusercontent.com/108851851/226197628-f97b2696-6b2f-427f-91fe-0ea52e4650a0.png">

5. Now let's save the Job by pressing Save in the top right corner.

## Run Your ETL Job
1. Select your job, `transform-csv-to-parquet`
2. Click **Run Job**

## Monitor and review your Job execution
1. Wait a few minutes while the job cycles through the following stages: Starting -> Running -> Stopped
2. To monitor the status of the job, click **Monitoring** in AWS Glue studio console and in “Running” click on “1” to view current job’s details and status.
<img width="1076" alt="image" src="https://user-images.githubusercontent.com/108851851/226198225-83b6d5af-633d-4ebe-8ec6-29d05458b3ca.png">
<img width="1078" alt="image" src="https://user-images.githubusercontent.com/108851851/226198244-b049e9d0-c74b-4ad4-9879-d3db2f5a53b4.png">
3. When the job is finished (i.e. in a Stopped state), open the Amazon S3 Console  and verify the transformed files are now in your Amazon S3 bucket under the path s3://awshk-industrial-forum-2023-{aws-account-number}/mytable-parquet/
<img width="1071" alt="image" src="https://user-images.githubusercontent.com/108851851/226198492-cc5e5e72-012f-4b4e-ba03-b88f2587edef.png">

## Check the difference with Athena
1. Open **Athena Console**
2. Open **Query editor**, click Refresh icon next to Data
3. In Database, select `ecommerce-data`
4. Run the following Query
```SQL
SELECT * FROM "ecommerce-data"."mytable" where Month = 'Feb';
```
5. Click + sign on the top right hand corner of the query editor
6. Run the following Query on the new editor
```SQL
SELECT * FROM "ecommerce-data"."mytable-parquet" where Month = 'Feb';
```
7. You can observe that data scanned from transformed data is much lower. 
- Parquet is a more storage efficient format for columnarized data
- Compression in the Glue job further reduced data size
- Partition on `Month` allows Athena query engine to on scan data in the correct partitions
