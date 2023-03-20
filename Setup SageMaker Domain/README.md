# Overview
After previous labs, you are having a datalake on AWS. AWS offers you AIML services to explore insight from your data. 
In the second part of today's workshop, we are going to use Amazon SageMaker Canvas. Let's prepare the environment before starting second part.

# Setup Studio Domain
1. Navigate to **SageMaker Console**
2. Click **Domain** on the left menu
3. Click Create domain
4. Choose **Quick setup**, set `industrial-forum` as Domain name
5. Choose `TeamRole` as Execution Role
6. Enable SageMaker Canvas permissions
<img width="812" alt="image" src="https://user-images.githubusercontent.com/108851851/226242505-fa2e02a2-a696-4456-87fe-f311d2b08837.png">

6. Click **Submit**
7. Wait for the Status to be **InService**

# Setup IAM Permission
1. Navigate to **IAM Console**
2. Click **Roles** on the left menu
3. Search for `TeamRole`
4. Click **Add permissions**, choose **Attach policies**
5. Tick **AmazonSageMakerCanvasFullAccess**, click **Add permissions**.

# Setup CORS Policy to the S3 bucket
SageMaker Canvas provides the capability to upload data stored locally to S3 via the Canvas UI. In order to do so, a CORS policy has to applied to the S3 bucket where you want to upload data (Canvas documentation  explains this in detail, if you want to learn more). Use the following procedure:

1. First of all, head over to the S3 Console  and identify your SageMaker default bucket or any other bucket you'd like to use. In our case, we will choose the bucket called `sagemaker-[AWS-REGION]-[ACCOUNT-ID]`.
2. Select it, then head over to the **Permissions**, and navigate until you reach the **Cross-origins resource sharing (CORS)**. Choose **Edit**.
3. Add the following CORS policy:
```JSON
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "POST"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": []
    }
]

```
4. Choose **Save changes**

# Setup Canvas Permission
1. Navigate to **SageMaker Console**
2. Click **Domain** on the left menu
3. Click the `industrial-forum` domain
4. Navigate to **Domain settings**, click **Edit**.
<img width="1101" alt="image" src="https://user-images.githubusercontent.com/108851851/226245024-f8940284-c781-44ec-b1b1-d23c0c4d58c0.png">

5. Navigate to **Step 4 Canvas Settings**
6. Under session **Canvas base permissions configuration**, make sure it is enabled
<img width="881" alt="image" src="https://user-images.githubusercontent.com/108851851/226245125-486beec2-c7be-416b-8a4d-b71f4c7dd165.png">

7. Scroll down, under **Local file upload configuration**, enable **Enable local file upload**
8. Click Submit

**Congratulation, you have setup the environment needed for using SageMaker Canvas.**
