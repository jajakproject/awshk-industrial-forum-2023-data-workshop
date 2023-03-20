
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
