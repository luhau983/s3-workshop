---
title : "Tạo EC2 Instance"
date : "`r Sys.Date()`"
weight : 2
chapter : false
description: "Hướng dẫn từng bước để tạo và cấu hình một EC2 instance trên AWS."
pre : " <b> 2.3 </b> "
---

## Tạo EC2 Instance

Amazon **EC2** (Elastic Compute Cloud) cho phép bạn chạy các máy chủ ảo trên đám mây. 
Hướng dẫn này sẽ hướng dẫn bạn qua các bước để khởi chạy và cấu hình một **EC2 Instance**.

### Bước 1: Điều hướng đến Dịch vụ EC2

1. Trong AWS Management Console, tìm kiếm "EC2" trong thanh tìm kiếm hoặc điều hướng đến **Services** > **EC2** để mở bảng điều khiển EC2.
   ![step1](/images/2.prerequisite/ec2/step1.png)

### Bước 2: Khởi chạy một Instance

Trong bảng điều khiển EC2, nhấp vào nút **Launch Instance** để bắt đầu quá trình tạo instance.
![Launch Instance](/images/2.prerequisite/ec2/step2.png)

1. Nhập tên cho **EC2 Instance**
   ![Launch Instance](/images/2.prerequisite/ec2/step2.2.png)

### Bước 3: Chọn Amazon Machine Image (AMI)

1. Chọn một **AMI** (Amazon Machine Image) cho instance của bạn. Image này cung cấp hệ điều hành và cấu hình phần mềm cho instance của bạn.
2. Bạn có thể chọn từ nhiều loại AMI khác nhau, bao gồm Amazon Linux, Ubuntu, Windows, v.v.
    - Tìm các AMI được đánh dấu là "Free Tier Eligible" để tận dụng các lợi ích của free Tier Eligible, cung cấp sử dụng giới hạn mà không tốn phí.
      ![Select AMI](/images/2.prerequisite/ec2/step3.png)

### Bước 4: Chọn Loại Instance

1. Chọn loại instance phù hợp với yêu cầu của bạn. Các loại instance khác nhau về CPU, bộ nhớ, lưu trữ và networking.
2. Đối với mục đích chung, bạn có thể chọn loại instance như `t2.micro` (đủ điều kiện cho lớp miễn phí).
   ![Choose Instance Type](/images/2.prerequisite/ec2/step4.png)
3. Tạo một cặp khóa mới hoặc sử dụng một cặp khóa hiện có. Cặp khóa này được sử dụng để kết nối an toàn với instance của bạn qua SSH.
   ![KeyPair](/images/2.prerequisite/ec2/step4.3.png)

### Bước 5: Cấu hình Instance

1. Cấu hình chi tiết của instance, bao gồm số lượng instance, mạng và cài đặt subnet.
2. Đặt thêm các tùy chọn nếu cần, chẳng hạn như vai trò IAM hoặc giám sát.

   ![Configure Instance](/images/2.prerequisite/ec2/step5.png)

### Bước 6: Thêm Lưu trữ

1. Thêm các khối lưu trữ vào instance của bạn nếu cần. Cài đặt mặc định thường bao gồm một volume gốc.
2. Bạn có thể gắn thêm các volume EBS (Elastic Block Store) nếu cần.

### Bước 8: Thêm Thẻ (Tùy chọn)

1. Thêm thẻ vào instance của bạn để giúp tổ chức và quản lý nó. Các thẻ là các cặp khóa-giá trị có thể được sử dụng để theo dõi chi phí, tự động hóa và nhận diện.

### Bước 9: Xem lại và Khởi chạy

1. Xem lại cấu hình instance của bạn để đảm bảo mọi thứ đều chính xác.
2. Nhấp vào **Launch** để bắt đầu quá trình tạo instance.
3. Bạn sẽ được yêu cầu chọn một cặp khóa hiện có hoặc tạo một cặp mới. Cặp khóa này được sử dụng để kết nối an toàn với instance của bạn qua SSH.

### Bước 11: Truy cập Instance của Bạn

1. Khi instance đã được khởi chạy, quay lại bảng điều khiển EC2 và chọn **Instances** để xem instance mới của bạn.
2. Sử dụng địa chỉ IP công cộng hoặc tên DNS của instance để kết nối với nó.

    - Đối với các instance Linux, kết nối bằng SSH: `ssh -i "your-key.pem" ec2-user@your-instance-public-dns`
    - Đối với các instance Windows, sử dụng RDP (Remote Desktop Protocol) với các thông tin đăng nhập được cung cấp.

### Kết luận

Bạn đã tạo và khởi chạy thành công một **EC2 Instance**. Bạn có thể cấu hình và sử dụng instance của mình theo nhu cầu cho ứng dụng hoặc các nhiệm vụ phát triển.

Để biết thêm chi tiết và cấu hình nâng cao, hãy tham khảo [Tài liệu EC2 của AWS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html).
