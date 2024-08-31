---
title : "Create IAM User"
date : "`r Sys.Date()`"
weight : 2
chapter : false
description: "Detailed steps for creating an IAM user in AWS."
pre : " <b> 2.2 </b> "
---

## Creating an IAM User

In this step, we will proceed to create IAM Role. In this IAM Role, the policy **AmazonSSMManagedInstanceCore** will be assigned, this is the policy that allows the EC2 server to communicate with the Session Manager.

### Step 1: Access IAM Service

In the AWS Management Console, type "IAM" into the search bar or navigate to **Services** > **IAM** to open the IAM dashboard.
![step1](/images/2.prerequisite/iam/step1.png)

### Step 2: Start Creating a New User

1. In the IAM dashboard, select **Users** from the left-hand menu.
2. Click the **Add user** button to begin the user creation process.
![step2](/images/2.prerequisite/iam-user/step2.png)
3. Enter a user name. Then click Next button
![step2.1](/images/2.prerequisite/iam-user/step2.1.png)
![step2.2](/images/2.prerequisite/iam-user/step2.2.png)
- Click Create user button
![step2.2](/images/2.prerequisite/iam-user/step2.3.png)