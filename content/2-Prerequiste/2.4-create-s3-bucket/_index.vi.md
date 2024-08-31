---
title: "Tạo S3 Bucket"
date: 2024-08-30
description: "Hướng dẫn từng bước để tạo và cấu hình một S3 bucket trong AWS."
type: "post"
draft: false
pre : " <b> 2.4 </b> "
---

## Tạo S3 Bucket

Amazon S3 (Simple Storage Service) là một dịch vụ lưu trữ có thể mở rộng cho phép bạn lưu trữ và truy xuất bất kỳ số lượng dữ liệu nào từ bất kỳ đâu. Hướng dẫn này sẽ dẫn bạn qua các bước để tạo và cấu hình một **S3 bucket**.

### Bước 1: Điều hướng đến Dịch vụ S3

1. Trong AWS Management Console, tìm kiếm "S3" trong thanh tìm kiếm hoặc điều hướng đến **Services** > **S3** để mở bảng điều khiển S3.
   ![step1](/images/2.prerequisite/s3/step1.png)

### Bước 2: Tạo một Bucket Mới

1. Trong bảng điều khiển S3, nhấp vào nút **Create bucket** để bắt đầu quá trình tạo bucket.

   ![Create Bucket](/images/2.prerequisite/s3/step2.png)

### Bước 3: Cấu hình Cài đặt Bucket

1. **Bucket Name**: Nhập một tên duy nhất cho bucket của bạn. Tên bucket phải là duy nhất toàn cầu trên tất cả các vùng AWS.
2. **Region**: Chọn vùng AWS nơi bạn muốn tạo bucket. Hãy xem xét việc chọn một vùng gần với người dùng mục tiêu của bạn để giảm độ trễ.

   ![Bucket Settings](/images/2.prerequisite/s3/step3.png)

### Bước 4: Cấu hình Tùy chọn Bucket

1. **Object Ownership**:
   - Chọn giữa **ACLs disabled** (khuyến nghị) hoặc **ACLs enabled** dựa trên trường hợp sử dụng của bạn. Việc vô hiệu hóa ACLs đơn giản hóa quyền truy cập bằng cách chỉ sử dụng chính sách bucket cho kiểm soát quyền truy cập.
     ![Object Ownership](/images/2.prerequisite/s3/step4.png)

2. **Block Public Access Settings**:
   - Mặc định, Amazon S3 chặn quyền truy cập công khai vào bucket của bạn. Giữ cài đặt này bật để bảo vệ dữ liệu của bạn trừ khi bạn cần làm cho bucket của bạn có thể truy cập công khai.

   ![Public Access Settings](/images/2.prerequisite/s3/step5.png) <!-- Thay thế bằng liên kết hình ảnh thực tế nếu có -->

3. **Bucket Versioning**:
   - Bật phiên bản hóa để giữ nhiều phiên bản của một đối tượng trong cùng một bucket. Điều này hữu ích cho sao lưu và phục hồi dữ liệu.

4. **Tags**:
   - Thêm thẻ vào bucket của bạn để tổ chức và quản lý nó hiệu quả hơn. Thẻ là các cặp khóa-giá trị có thể được sử dụng để theo dõi chi phí, tự động hóa và nhận diện.

5. **Default Encryption**:
   - Bật mã hóa mặc định để tự động mã hóa tất cả các đối tượng lưu trữ trong bucket. Bạn có thể chọn giữa các khóa do AWS quản lý (SSE-S3) hoặc Dịch vụ Quản lý Khoá AWS (SSE-KMS) để mã hóa.

6. **Advanced Settings**:
   - Cấu hình ghi nhật ký, khóa đối tượng và các cài đặt nâng cao khác nếu cần. Những tùy chọn này thường được sử dụng cho các trường hợp sử dụng đặc biệt hơn.

### Bước 5: Xem lại và Tạo

1. Xem lại tất cả các cấu hình bạn đã thiết lập cho bucket để đảm bảo chúng đáp ứng yêu cầu của bạn.
2. Nhấp vào **Create bucket** để hoàn tất việc tạo.

   ![Review and Create](/images/2.prerequisite/s3/step6.png) 
