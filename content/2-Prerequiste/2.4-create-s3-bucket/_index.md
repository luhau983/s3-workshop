---
title: "Creating an S3 Bucket"
date: 2024-08-30
description: "Step-by-step guide to creating and configuring an S3 bucket in AWS."
type: "post"
draft: false
pre : " <b> 2.4 </b> "
---

## Creating an S3 Bucket

Amazon S3 (Simple Storage Service) is a scalable storage service that allows you to store and retrieve any amount of data from anywhere. This guide will walk you through the steps to create and configure an S3 bucket.

### Step 1: Navigate to S3 Service

1. In the AWS Management Console, search for "S3" in the search bar or navigate to **Services** > **S3** to open the S3 dashboard.
   ![step1](/images/2.prerequisite/s3/step1.png)

### Step 2: Create a New Bucket

1. In the S3 dashboard, click the **Create bucket** button to start the bucket creation process.

   ![Create Bucket](/images/2.prerequisite/s3/step2.png)

### Step 3: Configure Bucket Settings

1. **Bucket Name**: Enter a unique name for your bucket. Bucket names must be globally unique across all AWS regions.
2. **Region**: Choose the AWS region where you want to create the bucket. Consider selecting a region close to your target users to reduce latency.

   ![Bucket Settings](/images/2.prerequisite/s3/step3.png)

### Step 4: Configure Bucket Options

1. **Object Ownership**:
   - Choose between **ACLs disabled** (recommended) or **ACLs enabled** based on your use case. Disabling ACLs simplifies permissions by using only bucket policies for access control.
   ![Object Ownership](/images/2.prerequisite/s3/step4.png)

2. **Block Public Access Settings**:
   - By default, Amazon S3 blocks public access to your bucket. Keep this setting enabled to protect your data unless you specifically need to make your bucket publicly accessible.

   ![Public Access Settings](/images/2.prerequisite/s3/step5.png)  

3. **Bucket Versioning**:
   - Enable versioning to keep multiple versions of an object in the same bucket. This is useful for data backups and recovery.

4. **Tags**:
   - Add tags to your bucket to organize and manage it more effectively. Tags are key-value pairs that can be used for cost tracking, automation, and identification.

5. **Default Encryption**:
   - Enable default encryption to automatically encrypt all objects stored in the bucket. You can choose between AWS-managed keys (SSE-S3) or AWS Key Management Service (SSE-KMS) for encryption.

6. **Advanced Settings**:
   - Configure logging, object lock, and other advanced settings if needed. These options are generally used for more specialized use cases.

### Step 5: Review and Create

1. Review all the configurations you've set for the bucket to ensure they meet your requirements.
2. Click **Create bucket** to finalize the creation.

   ![Review and Create](/images/2.prerequisite/s3/step6.png)  
