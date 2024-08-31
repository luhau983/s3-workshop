---
title : "Create IAM Role"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.1 </b> "
---

## Creating IAM Role

In this section, we will walk through the process of creating an IAM (Identity and Access Management) role that will be used to grant permissions to our EC2 instance for interacting with AWS S3. IAM roles are crucial for securely managing access to AWS resources.

### Step 1: Sign in to AWS Management Console

1. Go to the [AWS Management Console](https://aws.amazon.com/console/).
2. Sign in using your AWS account credentials.

### Step 2: Navigate to IAM Service

1. In the AWS Management Console, type "IAM" into the search bar or navigate to **Services** > **IAM** to open the IAM dashboard.
![step1](/images/2.prerequisite/iam/step1.png)


### Step 3: Create a New Role

1. In the IAM dashboard, select **Roles** from the left-hand menu.
2. Click the **Create role** button.
![step2](/images/2.prerequisite/iam/step2.png)

### Step 4: Select Trusted Entity Type

1. Choose **AWS service** as the trusted entity type.
2. For the use case, select **EC2**. This allows EC2 instances to assume the role.
![step4](/images/2.prerequisite/iam/step4.png)
### Step 5: Attach Policies

1. Click the **Next: Permissions** button.
2. On the permissions page, you need to attach policies that grant permissions to access S3. You can choose an existing policy like `AmazonS3FullAccess` or create a custom policy if specific permissions are required.
    - **AmazonS3FullAccess**: Grants full access to all S3 buckets.
    - **Custom Policy**: If you prefer fine-grained control, click on **Create policy** and define your custom permissions using the JSON editor or the visual editor.
![step5](/images/2.prerequisite/iam/step5.png)

### Step 6: Review and Name the Role
1. Click the **Next: Tags** button to add tags to the role (optional).
2. Click the **Next: Review** button.
3. Enter a name for the role in the **Role name** field. For example, `EC2-S3-Role`.
4. Click the **Create role** button to create the IAM role.
![step6](/images/2.prerequisite/iam/step6.png)

### Step 7: Attach Policies
1. After successfully creating an IAM role, you may need to attach an inline policy to further customize the permissions associated with the role. Inline policies are policies that are embedded directly into a single IAM role, group, or user.
![step7](/images/2.prerequisite/iam/step7.png)
2. You need to attach policies that grant permissions to access S3 and Secrets Manager. You can choose existing policies or create a custom policy.

   - **AmazonS3FullAccess**: Grants full access to all S3 buckets.
   - **SecretsManagerReadOnly**: Grants read-only access to Secrets Manager secrets.
![step7.1](/images/2.prerequisite/iam/step7.1.png)
Here’s an example of a custom policy JSON that grants specific S3 and Secrets Manager actions:
```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "CombinedPermissions",
         "Effect": "Allow",
         "Action": [
           "secretsmanager:GetSecretValue",
           "s3:ListBucket",
           "s3:GetObject",
           "s3:PutObject",
           "s3:DeleteObject"
         ],
         "Resource": [
           "arn:aws:secretsmanager:us-east-1:017820676824:secret:upload-image-to-s3-secret-8UsdOW",
           "arn:aws:s3:::your-bucket-name",
           "arn:aws:s3:::your-bucket-name/*"
         ]
       }
     ]
   }
```
![step7.2](/images/2.prerequisite/iam/step7.2.png)

