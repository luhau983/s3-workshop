---
title : "Thiết Lập AWS Secrets Manager"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.2. </b> "
---
Hướng dẫn này sẽ hướng dẫn bạn cách thiết lập AWS Secrets Manager để quản lý các thông tin bí mật của ứng dụng của bạn.

## Bước 1: Tạo Một Bí Mật Trong AWS Secrets Manager
Nhấp vào **Store a new secret**.
![step1](/images/3.connect/sm/step1.png)
![step2](/images/3.connect/sm/step2.png)
Chọn **Other type of secrets.**
![step2](/images/3.connect/sm/step3.png)
Nhập các cặp **key-value** sau cho thông tin đăng nhập AWS và tên bucket của bạn:
![step4](/images/3.connect/sm/step4.png)
Cung cấp một tên cho thông tin bảo mật của bạn (ví dụ: mySpringBootAppSecrets).
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
Nhấn Next.
![step6](/images/3.connect/sm/step6.png)
Đánh giá các chi tiết để tạo Secrets Manager. Nhấp vào nút **Lưu** sau khi xem xét.
![step7](/images/3.connect/sm/step7.png)
![step7.1](/images/3.connect/sm/step7.1.png)




