---
title : "Preparation "
date : "`r Sys.Date()`"
weight : 2
chapter : false
description: "Preparing the infrastructure for AWS S3 Integration"
pre : " <b> 2. </b> "
---

## Preparation
{{% notice info %}}
In this section, we will prepare the necessary infrastructure on AWS. This involves setting up a Virtual Private Cloud (VPC) and launching an EC2 instance that will serve as the host for our backend application. Additionally, we will create an S3 bucket for storing images and configure the required IAM roles and users to secure and manage access to these resources.
{{% /notice %}}
### Content

#### [2.1 Creating IAM Role](2.1-createiamrole/)

An **IAM Role** is essential for granting your EC2 instance permissions to interact with other AWS services, such as S3. This role will be associated with the EC2 instance, enabling it to upload, retrieve, and delete files in your S3 bucket. We will create a role with the necessary policies and attach it to our EC2 instance.

#### [2.2 Create IAM User](2.2-create-iam-user)

An **IAM User** will be created to allow programmatic access to AWS services. This user will have specific permissions that limit access to only the resources required for this workshop, following the principle of least privilege. We will generate access keys for this user, which will be used in the backend application to interact with AWS services securely.

#### [2.3 Create EC2 Instance](2.3-create-ec2)

Next, we will launch an **EC2 Instance** that will host our backend application. This involves selecting the appropriate Amazon Machine Image (AMI), configuring security groups, and attaching the IAM role we created earlier. We will also install the necessary software, such as Java and Spring Boot, to run our application.

#### [2.4 Create S3 Bucket](2.4-create-s3-bucket)

An **S3 Bucket** will be created to store the images that our application will manage. We will configure the bucket with the appropriate permissions, enabling the backend application to upload, retrieve, and delete images. Additionally, we will explore advanced S3 features, such as bucket policies, encryption, and versioning, to ensure our data is secure and compliant with best practices.
