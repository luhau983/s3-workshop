---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

Chào mừng bạn đến với workshop toàn diện về việc tích hợp **AWS S3** với ứng dụng backend và triển khai nó trên một phiên bản **Amazon EC2**. Workshop này sẽ hướng dẫn bạn qua từng bước từ việc thiết lập cơ sở hạ tầng đám mây đến việc triển khai một ứng dụng hoàn chỉnh tương tác với các dịch vụ của AWS.

Dù bạn là một nhà phát triển backend với kinh nghiệm đang muốn mở rộng kỹ năng đám mây của mình hay là người mới bắt đầu làm quen với AWS, workshop này sẽ cung cấp cho bạn những kinh nghiệm thực tiễn và kiến thức hữu ích. Tôi sẽ bao quát mọi khía cạnh từ việc tạo và quản lý tài nguyên AWS đến việc tích hợp ứng dụng backend của bạn với S3, làm cho đây trở thành một hướng dẫn quan trọng cho bất kỳ ai muốn tận dụng AWS trong dự án của mình.

Kết thúc workshop, bạn sẽ có một cái nhìn toàn diện về cách sử dụng các dịch vụ AWS để xây dựng các ứng dụng có khả năng mở rộng, bảo mật và hiệu quả.

### Amazon EC2 - Amazon Elastic Compute Cloud
![AWS Logo](/images/ec2.png)
**Amazon EC2** là một phần quan trọng trong điện toán đám mây, cung cấp khả năng tính toán mở rộng trong đám mây. Nó cho phép bạn triển khai các máy chủ ảo, được gọi là instances, mà bạn có thể cấu hình với các hệ điều hành và phần mềm khác nhau để đáp ứng nhu cầu của bạn. Tính linh hoạt của EC2 làm cho nó trở thành lựa chọn lý tưởng cho việc lưu trữ ứng dụng web, chạy các hệ thống phân tán, hoặc thực hiện phân tích dữ liệu lớn.

Trong workshop này, tôi sẽ tập trung vào việc sử dụng EC2 để lưu trữ ứng dụng backend của bạn. Bạn sẽ học cách khởi tạo một instance EC2, cấu hình nó cho ứng dụng của bạn, và tận dụng các tính năng tự động mở rộng và cân bằng tải để đảm bảo ứng dụng của bạn có thể mở rộng và đáng tin cậy.

### Amazon S3 - Amazon Simple Storage Service
![AWS Logo](/images/s3.png)
**Amazon S3** là một trong những giải pháp lưu trữ đáng tin cậy và tiết kiệm nhất hiện nay. Nó cung cấp dịch vụ lưu trữ đối tượng có thể truy cập từ bất kỳ đâu trên thế giới, cho phép bạn lưu trữ và truy xuất bất kỳ lượng dữ liệu nào vào bất kỳ lúc nào. S3 được thiết kế với độ bền 99.999999999%, đảm bảo rằng dữ liệu của bạn luôn được bảo mật và sẵn sàng.

Trong workshop này, tôi sẽ sử dụng S3 để quản lý và lưu trữ hình ảnh cho ứng dụng của bạn. Bạn sẽ học cách tạo một bucket S3, tải lên và truy xuất tệp, và quản lý quyền truy cập. Ngoài ra, tôi sẽ khám phá các tính năng như phiên bản S3, chính sách vòng đời, và các cài đặt bảo mật để giúp bạn quản lý dữ liệu hiệu quả hơn.

### AWS SDK - Bộ công cụ của bạn để làm việc với AWS
![AWS Logo](/images/sdk.png)
**AWS SDK** là một bộ công cụ mạnh mẽ giúp đơn giản hóa việc tương tác với các dịch vụ AWS từ ứng dụng của bạn. Nó cung cấp các API và thư viện cho nhiều ngôn ngữ lập trình khác nhau, cho phép bạn thực hiện các tác vụ như tải tệp lên S3, khởi chạy các instance EC2, và quản lý tài nguyên AWS ngay từ mã của bạn.

Trong workshop này, tôi sẽ sử dụng AWS SDK cho Java để tích hợp S3 vào ứng dụng backend của bạn. Điều này bao gồm việc thiết lập SDK, viết mã để tương tác với S3, và triển khai các tính năng như URL ký trước cho các tải lên an toàn. AWS SDK sẽ giúp bạn xây dựng các ứng dụng phức tạp và hỗ trợ đám mây một cách dễ dàng.

### AWS Secrets Manager
![AWS Logo](/images/secret-manager.png)
**AWS Secrets Manager** là một dịch vụ giúp bạn quản lý và truy xuất các thông tin bảo mật như thông tin xác thực và khóa API một cách an toàn. Dịch vụ này giúp bạn tránh phải mã hóa các thông tin nhạy cảm trong ứng dụng, giảm rủi ro lộ thông tin và nâng cao bảo mật.

Tôi sẽ hướng dẫn bạn cách sử dụng Secrets Manager để lưu trữ và truy xuất các thông tin xác thực cần thiết để truy cập các dịch vụ AWS, chẳng hạn như các khóa để tương tác với S3. Bạn sẽ học cách tích hợp Secrets Manager với ứng dụng của bạn để truy cập thông tin bảo mật một cách an toàn, đảm bảo rằng ứng dụng của bạn tuân thủ các nguyên tắc bảo mật tốt nhất.
