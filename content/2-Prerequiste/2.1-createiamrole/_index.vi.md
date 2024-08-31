---
title : "Tạo Role IAM"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.1 </b> "
---

## Tạo Role IAM

Trong phần này, tôi sẽ hướng dẫn bạn quy trình tạo một **IAM** (Identity and Access Management) **role** mà sẽ được sử dụng để cấp quyền cho **EC2** của bạn để tương tác với **AWS S3**. Các **IAM** **roles** rất quan trọng để quản lý quyền truy cập vào các tài nguyên **AWS** một cách an toàn.

### Bước 1: Đăng nhập vào AWS Management Console

1. Truy cập [AWS Management Console](https://aws.amazon.com/console/).
2. Đăng nhập bằng thông tin tài khoản **AWS** của bạn.

### Bước 2: Điều hướng đến Service IAM

1. Trong **AWS Management Console**, gõ "IAM" vào thanh tìm kiếm hoặc điều hướng đến **Service** > **IAM** để mở bảng điều khiển **IAM**.
   ![step1](/images/2.prerequisite/iam/step1.png)

### Bước 3: Tạo Role Mới

1. Trong bảng điều khiển **IAM**, chọn **Role** từ menu bên trái.
2. Nhấp vào nút **Tạo role**.
   ![step2](/images/2.prerequisite/iam/step2.png)

### Bước 4: Chọn Loại Đối tượng Tin cậy

1. Chọn **Service AWS** làm loại đối tượng tin cậy.
2. Đối với trường hợp sử dụng, chọn **EC2**. Điều này cho phép các **EC2** đảm nhận role này.
   ![step4](/images/2.prerequisite/iam/step4.png)

### Bước 5: Gán Chính sách

1. Nhấp vào nút **Tiếp theo: Quyền**.
2. Trên trang quyền, bạn cần gán các chính sách cấp quyền truy cập **S3**. Bạn có thể chọn một chính sách hiện có như **AmazonS3FullAccess** hoặc tạo một chính sách tùy chỉnh nếu cần quyền truy cập cụ thể.
    - **AmazonS3FullAccess**: Cấp quyền truy cập đầy đủ cho tất cả các bucket **S3**.
    - **Chính sách Tùy chỉnh**: Nếu bạn muốn kiểm soát chi tiết, nhấp vào **Tạo chính sách** và định nghĩa quyền của bạn bằng cách sử dụng trình chỉnh sửa JSON hoặc trình chỉnh sửa trực quan.
      ![step5](/images/2.prerequisite/iam/step5.png)

### Bước 6: Xem lại và Đặt tên cho Role
1. Nhấp vào nút **Next: Tags** để thêm thẻ cho role (tùy chọn).
2. Nhấp vào nút **Next: Review**.
3. Nhập tên cho role trong trường **Role name**. Ví dụ: `EC2-S3-Role`.
4. Nhấp vào nút **Create role** để tạo role **IAM**.
   ![step6](/images/2.prerequisite/iam/step6.png)

### Bước 7: Gán Chính sách
1. Sau khi tạo thành công role **IAM**, bạn có thể cần gán một chính sách inline để tùy chỉnh thêm quyền liên quan đến role. Chính sách inline là các chính sách được nhúng trực tiếp vào một role **IAM**, nhóm, hoặc người dùng.
   ![step7](/images/2.prerequisite/iam/step7.png)
2. Bạn cần gán các chính sách cấp quyền truy cập **S3** và **Secrets Manager**. Bạn có thể chọn các chính sách hiện có hoặc tạo một chính sách tùy chỉnh.

    - **AmazonS3FullAccess**: Cấp quyền truy cập đầy đủ cho tất cả các bucket **S3**.
    - **SecretsManagerReadOnly**: Cấp quyền truy cập chỉ đọc cho các bí mật trong **Secrets Manager**.
      ![step7.1](/images/2.prerequisite/iam/step7.1.png)
      Dưới đây là ví dụ về chính sách tùy chỉnh JSON cấp quyền cho các hành động cụ thể trên **S3** và **Secrets Manager**:
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
