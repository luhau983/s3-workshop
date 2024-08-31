---
title : "Setup AWS Secrets Manager"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.2. </b> "
---
Hướng dẫn này sẽ hướng dẫn bạn cách thiết lập AWS Secrets Manager để quản lý các thông tin bí m  của ứng dụng của bạn.

## Bước 1: Tạo Một Bí Mật Trong AWS Secrets Manager
Click Store a new secret.
![step1](/images/3.connect/sm/step1.png)
![step2](/images/3.connect/sm/step2.png)
Choose Other type of secrets.
![step2](/images/3.connect/sm/step3.png)
Enter the following key-value pairs for your AWS credentials and bucket name:
![step4](/images/3.connect/sm/step4.png)
Provide a name for your secret (e.g., mySpringBootAppSecrets).
![step5](/images/3.connect/sm/step5.png)
![step5.1](/images/3.connect/sm/step5.1.png)
```json
{
"Version" : "2012-10-17",
"Statement" : [ {
 "Effect" : "Allow",
 "Principal" : {
   "AWS" : "arn:aws:iam::017820676824:role/ec2-role-for-s3-and-secret-management"
 },
 "Action" : "secretsmanager:GetSecretValue",
 "Resource" : "*"
} ]
}
```
Click Next.
![step6](/images/3.connect/sm/step6.png)
Evaluate the details for creating a Secrets Manager. You can inspect the sample code provided by AWS for configuring and executing your code to obtain the key. Click the "Store" button after reviewing
![step7](/images/3.connect/sm/step7.png)
![step7.1](/images/3.connect/sm/step7.1.png)




