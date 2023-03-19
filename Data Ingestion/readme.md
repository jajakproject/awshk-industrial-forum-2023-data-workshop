In this lab, you will use AWS CloudShell to run commands using the AWS CLI (Command Line Interface). The below command copies the contents of an Amazon S3 bucket into the S3 bucket in your AWS account. This simulates the action of batch-ingesting data into your S3 Data Lake.

1. In the AWS Console, navigate to AWS CloudShell  to trigger a new command line environment for you. Figure
2. After some time, you will see the AWS CloudShell console as per the screenshot above.
3. Copy and paste the following into CloudShell, which will automatically copy some content into your S3 bucket for this Immersion Day.

```
export MY_ACCOUNT_ID="$(aws sts get-caller-identity --query Account --output text)"
aws s3 mb s3://awshk-industrial-forum-2023-$MY_ACCOUNT_ID --region us-west-1
aws s3 cp s3://awshk-industrial-forum-2023/datalake "s3://awshk-industrial-forum-2023-$MY_ACCOUNT_ID/datalake" --recursive
```

