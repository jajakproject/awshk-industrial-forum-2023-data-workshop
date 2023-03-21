# Overview
Now that you have data in your data lake storage, let’s create a unified catalog for our data lake.

## Create crawler to auto discover schema of your data in S3
1. Open Glue Console, click **Crawlers**. Then click **Create crawler**.
<img width="974" alt="image" src="https://user-images.githubusercontent.com/108851851/226185529-21098a4a-7221-43a3-908a-15d6052a437e.png">

2. Click **Create Crawler**
- Set Crawler name to `industrial-forum` and click **Next**

3. On the Choose data sources and classifiers screen:
- Leave the "Data source configuration" as is
- Click **Add a data source**
4. On the **Add a data source** screen:
- Leave the `Data source` set to `S3`
- Click **Browse S3** and click on the name of the S3 bucket used for this Immersion Day, `s3://awshk-industrial-forum-{aws-account-number}`
- Click on the circle next to the `mytable` and select **Choose**
- Select the Crawl all sub-folders option and click **Add an S3 data source**
- Finally, click **Next**
5. On the **Configure security settings** screen:
- Click **Create new IAM role**
- On **Create new IAM role** screen, set IAM role name to `AWSGlueServiceRole-industrialforum` and click **Create**
- Wait a second for the role to be created, then click **Next**
<img width="838" alt="image" src="https://user-images.githubusercontent.com/108851851/226186427-2f942953-0773-4cfe-8fbe-ab3fc26e6c50.png">

6. On the **Set output and scheduling** screen:
- Click the **Add database** button which will open a new tab
- Type `ecommerce-data` into the Name under **Database details** and click **Create database**
- You can close this browser tab and switch back to the **Set output and scheduling** screen
- Click the refresh button looking like a circle to load the `ecommerce-data` database you just created and select it
- Under Crawler Schedule, leave it as `On demand` and click **Next**

7. On the **Review and create** screen of this crawler, review your settings and click **Create crawler**

8. Back in the Crawlers window, select your crawler, i.e. `industrial-forum`, and click **Run crawler**:
<img width="1142" alt="image" src="https://user-images.githubusercontent.com/108851851/226187582-02bcc1bf-8f78-4157-be85-a0edeab9891b.png">

9. Wait ~2 minutes for the crawler to finish. Once it completes, you should see a table change as displayed in the bottom right corner in the example below.
<img width="1119" alt="image" src="https://user-images.githubusercontent.com/108851851/226187777-89125b14-1c58-4cd7-85ad-a763ab7adc5c.png">

Congratulations, you are now ready to query your data on AWS with Athena.
