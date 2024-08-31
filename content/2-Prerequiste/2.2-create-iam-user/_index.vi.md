---
title : "Tạo Người dùng IAM"
date : "`r Sys.Date()`"
weight : 2
chapter : false
description: "Các bước chi tiết để tạo một User IAM trong AWS."
pre : " <b> 2.2 </b> "
---

## Tạo Người dùng IAM

Trong bước này, chúng ta sẽ tiến hành tạo một **IAM Role**. Trong **IAM Role** này, chính sách **AmazonSSMManagedInstanceCore** sẽ được gán, đây là chính sách cho phép máy chủ **EC2** giao tiếp với **Session Manager**.

### Bước 1: Truy cập Dịch vụ IAM

Trong **AWS Management Console**, gõ "IAM" vào thanh tìm kiếm hoặc điều hướng đến **Dịch vụ** > **IAM** để mở bảng điều khiển **IAM**.
![step1](/images/2.prerequisite/iam/step1.png)

### Bước 2: Bắt đầu Tạo Người dùng Mới

1. Trong bảng điều khiển **IAM**, chọn **Users** từ menu bên trái.
2. Nhấp vào nút **Add User** để bắt đầu quy trình tạo User.
   ![step2](/images/2.prerequisite/iam-user/step2.png)
3. Nhập tên User. Sau đó nhấp vào nút Tiếp theo
   ![step2.1](/images/2.prerequisite/iam-user/step2.1.png)
   ![step2.2](/images/2.prerequisite/iam-user/step2.2.png)
- Nhấp vào nút Create User
  ![step2.2](/images/2.prerequisite/iam-user/step2.3.png)
