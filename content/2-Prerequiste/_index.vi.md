---
title : "Chuẩn bị"
date : "`r Sys.Date()`"
weight : 2
chapter : false
description: "Chuẩn bị cơ sở hạ tầng cho tích hợp AWS S3"
pre : " <b> 2. </b> "
---

## Chuẩn bị
{{% notice info %}}
Trong phần này, chúng ta sẽ chuẩn bị cơ sở hạ tầng cần thiết trên AWS. Điều này bao gồm việc thiết lập một Virtual Private Cloud (VPC) và khởi chạy một **EC2 Instance** sẽ phục vụ như là máy chủ cho ứng dụng backend của chúng ta. Ngoài ra, chúng ta sẽ tạo một **S3 Bucket** để lưu trữ hình ảnh và cấu hình các **IAM Role** và người dùng cần thiết để bảo mật và quản lý quyền truy cập vào các tài nguyên này.
{{% /notice %}}
### Nội dung

#### [2.1 Tạo IAM Role](2.1-createiamrole/)

Một **IAM Role** là cần thiết để cấp quyền cho **EC2 Instance** của bạn tương tác với các dịch vụ AWS khác, chẳng hạn như **S3**. Vai trò này sẽ được liên kết với **EC2 Instance**, cho phép nó tải lên, lấy và xóa các tệp trong **S3 Bucket** của bạn. Chúng ta sẽ tạo một vai trò với các chính sách cần thiết và gán nó cho **EC2 Instance** của chúng ta.

#### [2.2 Tạo IAM User](2.2-create-iam-user)

Một **IAM User** sẽ được tạo để cho phép truy cập lập trình vào các dịch vụ AWS. Người dùng này sẽ có các quyền cụ thể giới hạn quyền truy cập chỉ vào các tài nguyên cần thiết cho hội thảo này, theo nguyên tắc tối thiểu quyền. Chúng ta sẽ tạo các khóa truy cập cho người dùng này, các khóa này sẽ được sử dụng trong ứng dụng backend để tương tác với các dịch vụ AWS một cách an toàn.

#### [2.3 Tạo EC2 Instance](2.3-create-ec2)

Tiếp theo, chúng ta sẽ khởi chạy một **EC2 Instance** để lưu trữ ứng dụng backend của chúng ta. Điều này bao gồm việc chọn Amazon Machine Image (AMI) phù hợp, cấu hình các nhóm bảo mật, và gán vai trò IAM mà chúng ta đã tạo trước đó. Chúng ta cũng sẽ cài đặt phần mềm cần thiết, chẳng hạn như Java và Spring Boot, để chạy ứng dụng của chúng ta.

#### [2.4 Tạo S3 Bucket](2.4-create-s3-bucket)

Một **S3 Bucket** sẽ được tạo để lưu trữ các hình ảnh mà ứng dụng của chúng ta sẽ quản lý. Chúng ta sẽ cấu hình bucket với các quyền phù hợp, cho phép ứng dụng backend tải lên, lấy và xóa hình ảnh. Ngoài ra, chúng ta sẽ khám phá các tính năng nâng cao của **S3**, chẳng hạn như chính sách bucket, mã hóa và phiên bản, để đảm bảo dữ liệu của chúng ta được bảo mật và tuân thủ các phương pháp tốt nhất.
