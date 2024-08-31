---
title : "Creating an EC2 Instance"
date : "`r Sys.Date()`"
weight : 2
chapter : false
description: "Step-by-step guide to creating and configuring an EC2 instance in AWS."
pre : " <b> 2.3 </b> "
---

## Creating an EC2 Instance

Amazon EC2 (Elastic Compute Cloud) allows you to run virtual servers in the cloud. This guide will walk you through the steps to launch and configure an EC2 instance.

### Step 1: Navigate to EC2 Service

1. In the AWS Management Console, search for "EC2" in the search bar or navigate to **Services** > **EC2** to open the EC2 dashboard.
![step1](/images/2.prerequisite/ec2/step1.png)
### Step 2: Launch an Instance

In the EC2 dashboard, click the **Launch Instance** button to start the instance creation process.
![Launch Instance](/images/2.prerequisite/ec2/step2.png)

1. Enter a name for EC2 Instance
![Launch Instance](/images/2.prerequisite/ec2/step2.2.png)

### Step 3: Choose an Amazon Machine Image (AMI)

1. Select an AMI (Amazon Machine Image) for your instance. This image provides the operating system and software configuration for your instance.
2. You can choose from a variety of AMIs, including Amazon Linux, Ubuntu, Windows, etc. 
- Look for AMIs marked as "Free Tier Eligible" to take advantage of the free tier benefits, which offer limited usage at no cost.
![Select AMI](/images/2.prerequisite/ec2/step3.png)
### Step 4: Choose an Instance Type

1. Select the instance type that matches your requirements. Instance types vary by CPU, memory, storage, and networking capacity.
2. For general purposes, you might choose an instance type like `t2.micro` (eligible for the free tier).
![Choose Instance Type](/images/2.prerequisite/ec2/step4.png)  
3. Create a new key pair or use an existing one. This key pair is used to securely connect to your instance via SSH.
![KeyPair](/images/2.prerequisite/ec2/step4.3.png)

### Step 5: Configure Instance

1. Configure the instance details, including the number of instances, network, and subnet settings.
2. Set additional options if needed, such as IAM roles or monitoring.

   ![Configure Instance](/images/2.prerequisite/ec2/step5.png)

### Step 6: Add Storage

1. Add storage volumes to your instance if required. The default settings usually include a root volume.
2. You can attach additional EBS (Elastic Block Store) volumes as needed.

### Step 8: Add Tags (Optional)

1. Add tags to your instance to help organize and manage it. Tags are key-value pairs that can be used for cost tracking, automation, and identification.

### Step 9: Review and Launch

1. Review your instance configuration to ensure everything is correct.
2. Click **Launch** to start the instance creation process.
3. You will be prompted to select an existing key pair or create a new one. This key pair is used to securely connect to your instance via SSH.

### Step 11: Access Your Instance

1. Once the instance is launched, go back to the EC2 dashboard and select **Instances** to view your new instance.
2. Use the public IP address or DNS name of the instance to connect to it.

    - For Linux instances, connect using SSH: `ssh -i "your-key.pem" ec2-user@your-instance-public-dns`
    - For Windows instances, use RDP (Remote Desktop Protocol) with the credentials provided.

### Conclusion

You have successfully created and launched an EC2 instance. You can now configure and use your instance as needed for your application or development tasks.

For further details and advanced configurations, refer to the [AWS EC2 Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html).
