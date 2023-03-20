# Setup QuickSight
1. Open QuickSight console, it will ask you to Sign up. Click **Sign up for QuickSight**.
<img width="620" alt="image" src="https://user-images.githubusercontent.com/108851851/226199259-a40192af-9a7c-43d0-bdcb-bb49353e3a1d.png">

2. Choose the Enterprise edition and click **Continue**.
3. On the Amazon QuickSight account creation settings page, use the values below:
  - Select the same region you created the AWS Glue data catalog database in, otherwise Amazon QuickSight will not be able to see them.
  - Set your Amazon QuickSight account name. Notice: This must be a globally unique value across all AWS accounts and regions. If you find a name that's unavailable simply try again with a different name.
  - Enter your email address as **Notification email address**.
  - **Enable auto discovery of data and users....**
  - Select **Amazon Athena**.
  - Select **Amazon S3** which will trigger a window to open.
    - On the popup, the first tab will show your Amazon S3 buckets in that region. Select your datalake bucket, `s3://awshk-industrial-forum-2023-{aws-account-number}`
4. Now you can click Finish to complete the set up of your Amazon QuickSight instance.
5. Wait untill you see this message:
<img width="534" alt="image" src="https://user-images.githubusercontent.com/108851851/226199620-17028922-f1db-4cb5-8648-4b53f288ce4d.png">

6. Click **Go to Amazon QuickSight** to start visualizing your data.

# Add Athena dataset
1. Click on **Data Sets** in the left menu.
2. Then click the **New dataset** button on the top of the window.
3. Under From New Data Sources, click **Athena**
4. Give your datasource a name, such as `athena` and click **Create data source**.
5. On the Choose your table window, select the `ecommerce-data` database that you created during data ingestion, select the mytable-parquet table, and click the Edit/Preview data button.
6. You should now see a similar screen.
<img width="1413" alt="image" src="https://user-images.githubusercontent.com/108851851/226230626-95253414-2e42-4dd5-8130-72fdd9f14059.png">

7. In the previous step you created a link between Amazon QuickSight and the streaming data you ingested in Lab 1. You are now in the edit/preview window of your dataset. Notice that you can re-order, rename, drop, and perform certain other preparation tasks on your data prior to visualizing it.
8. Click the **Publish & visualize** button to be brought to the "Analysis" window where you can start creating your dashboard.
9. Choose **Interactive sheet**
10. In the lower left, set the Visual type to Horizontal bar chart (you must hover over the shapes to see their names).
11. From the Field list, drag the department column to the Y-Axis box.
12. From the Field list, drag the price column to the Value box.
13. From the Field list, drag the product column to the Group/Color box.
14. Left-click one of the horizontal bars in the chart and choose Focus only on ... (just to demo drill-down features)
15. Your visualization should look something like the following:
