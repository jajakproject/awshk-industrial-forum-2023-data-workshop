In this lab, you will use AWS CloudShell to run commands using the AWS CLI (Command Line Interface). The below command copies the contents of an Amazon S3 bucket into the S3 bucket in your AWS account. This simulates the action of batch-ingesting data into your S3 Data Lake.

1. In the AWS Console, navigate to AWS CloudShell  to trigger a new command line environment for you. 
<img width="1022" alt="image" src="https://user-images.githubusercontent.com/108851851/226184546-44ed3634-3f82-4f42-ae48-a62452e7682f.png">

2. After some time, you will see the AWS CloudShell console as per the screenshot above.
3. Copy and paste the following into CloudShell, which will automatically copy some content into your S3 bucket for this Immersion Day.

```
mkdir datalake
cd datalake
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/Feb.csv
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/Mar.csv
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/May.csv
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/Oct.csv
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/June.csv
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/Jul.csv
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/Aug.csv
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/Nov.csv
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/Sep.csv
wget https://d3b1pahv6e8ff3.cloudfront.net/datalake/Dec.csv

export MY_ACCOUNT_ID="$(aws sts get-caller-identity --query Account --output text)"
aws s3 mb s3://awshk-industrial-forum-2023-$MY_ACCOUNT_ID --region us-west-1

cd ..
aws s3 cp datalake/ "s3://awshk-industrial-forum-2023-$MY_ACCOUNT_ID/mytable" --recursive

```

4. You should see this screen when all the commands finish
<img width="759" alt="image" src="https://user-images.githubusercontent.com/108851851/226187129-d5637016-1fa6-4edf-898d-3a88eb48b59f.png">

5. Go to S3 console, you should find a bucket called **awshk-industrial-forum-2023-\<Your AWS Account ID\>**
<img width="1064" alt="image" src="https://user-images.githubusercontent.com/108851851/226185121-e5738b19-351e-485d-8e45-216c5e83e43d.png">

6. Click into the bucket, you should find a folder called table and there are 10 csv files inside.
<img width="1080" alt="image" src="https://user-images.githubusercontent.com/108851851/226185195-5ccb2ec4-c199-46a8-8d05-e496e41a9ed8.png">
