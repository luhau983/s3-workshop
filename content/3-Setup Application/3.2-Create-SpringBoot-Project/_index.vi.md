---
title: "Thiết Lập Dự Án Spring Boot"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

Làm theo các bước sau để thiết lập một dự án Spring Boot tích hợp với AWS S3 từ máy tính của bạn.

## Bước 1: Tạo Dự Án Spring Boot Mới

1. **Sử dụng Spring Initializr**:
    - Truy cập [Spring Initializr](https://start.spring.io/).
    - Cài đặt chi tiết dự án và thêm các dependencies cần thiết (Spring Web, Spring Boot DevTools, AWS SDK S3).
    - Nhấn **Generate** để tải xuống dự án.
    - Giải nén tệp và mở nó trong IDE của bạn.

## Bước 2: Thêm Các Phụ Thuộc AWS SDK

Nếu không được thêm trong quá trình thiết lập dự án, thêm các dependencies sau vào `pom.xml`:

```xml
<dependency>
    <groupId>software.amazon.awssdk</groupId>
    <artifactId>s3</artifactId>
</dependency>
<dependency>
    <groupId>software.amazon.awssdk</groupId>
    <artifactId>auth</artifactId>
</dependency>
<dependency>
    <groupId>software.amazon.awssdk</groupId>
    <artifactId>regions</artifactId>
</dependency>
```
## Step 3: Configure AWS Credentials
**.AwsConfig.class**.
Lớp này sẽ cấu hình client S3 sử dụng thông tin đăng nhập được lấy từ Secrets Manager:

```java
package com.example.demo.config;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import software.amazon.awssdk.auth.credentials.AwsBasicCredentials;
import software.amazon.awssdk.auth.credentials.AwsCredentialsProvider;
import software.amazon.awssdk.auth.credentials.StaticCredentialsProvider;
import software.amazon.awssdk.regions.Region;
import software.amazon.awssdk.services.secretsmanager.SecretsManagerClient;
import software.amazon.awssdk.services.s3.S3Client;
import software.amazon.awssdk.services.secretsmanager.model.GetSecretValueRequest;
import software.amazon.awssdk.services.secretsmanager.model.GetSecretValueResponse;

@Configuration
public class AwsConfig {

    @Value("${aws.secretsmanager.secret.id}")
    private String secretId;

    @Value("${aws.region}")
    private String region;

    @Bean
    public SecretsManagerClient secretsManagerClient() {
        return SecretsManagerClient.builder()
                .region(Region.of(region))
                .build();
    }

    @Bean
    public S3Client s3Client(SecretsManagerClient secretsManagerClient) {
        String secretString = getSecret(secretsManagerClient);
        AwsCredentialsProvider credentialsProvider = StaticCredentialsProvider.create(
                AwsBasicCredentials.create(
                        extractValue(secretString, "aws.access.key.id"),
                        extractValue(secretString, "aws.secret.access.key")
                )
        );

        return S3Client.builder()
                .region(Region.of(region))
                .credentialsProvider(credentialsProvider)
                .build();
    }

    private String getSecret(SecretsManagerClient secretsManagerClient) {
        GetSecretValueRequest request = GetSecretValueRequest.builder()
                .secretId(secretId)
                .build();

        GetSecretValueResponse response = secretsManagerClient.getSecretValue(request);
        return response.secretString();
    }

    private String extractValue(String secretString, String key) {
        String[] entries = secretString.split(",");
        for (String entry : entries) {
            if (entry.contains(key)) {
                return entry.split(":")[1].replaceAll("[\"{}]", "").trim();
            }
        }
        throw new RuntimeException("Key not found in secret string");
    }
}
```

**S3Service.class**
Lớp này sẽ sử dụng client S3 để tải lên các tệp vào bucket S3:
```java
package com.example.demo.service;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;
import software.amazon.awssdk.core.sync.RequestBody;
import software.amazon.awssdk.services.s3.S3Client;
import software.amazon.awssdk.services.s3.model.PutObjectRequest;
import java.io.ByteArrayInputStream;

@Service
public class S3Service {

    private final S3Client s3Client;

    @Value("${s3.bucket.name}")
    private String bucketName;

    public S3Service(S3Client s3Client) {
        this.s3Client = s3Client;
    }

    public void uploadFile(String key, byte[] content) {
        PutObjectRequest putObjectRequest = PutObjectRequest.builder()
                .bucket(bucketName)
                .key(key)
                .build();

        s3Client.putObject(putObjectRequest, RequestBody.fromInputStream(new ByteArrayInputStream(content), content.length));
    }
}
```

## Step 6: Create a REST Controller
Create a REST controller to expose an endpoint for file uploads:

```java
package com.example.demo.controller;

import com.example.demo.service.S3Service;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class FileUploadController {

    private final S3Service s3Service;

    public FileUploadController(S3Service s3Service) {
        this.s3Service = s3Service;
    }

    @PostMapping("/upload")
    public String uploadFile(@RequestParam("key") String key, @RequestParam("file") byte[] file) {
        s3Service.uploadFile(key, file);
        return "File uploaded successfully!";
    }
}

```
## Step 7: Test API Locally with Postman
1. Khởi động ứng dụng Spring Boot của bạn bằng cách chạy main class hoặc IDE’s run configuration.
2. Sử dụng công cụ như Postman hoặc curl để gửi request POST:

- Method: POST
- URL: http://localhost:8080/upload
- Body: Select form-data and add the following fields:
- key: Your file key (e.g., test.txt)
- file: Choose a file to upload

```bash
curl -F "file=@path/to/your/file" http://localhost:8080/upload
```
- Nhấn Gửi và xác minh phản hồi: "File uploaded successfully!".
3. Verify Upload:
   Xác minh Tải Lên: Kiểm tra bucket S3 của bạn qua AWS Management Console để đảm bảo tệp đã được tải lên thành công.
4. Xác minh URL phản hồi để đảm bảo nó trỏ đến tệp đúng trong S3.
