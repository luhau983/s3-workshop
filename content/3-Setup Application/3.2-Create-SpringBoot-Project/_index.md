---
title : "Spring Boot Project Setup"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---
Follow these steps to set up a Spring Boot project integrated with AWS S3 from your local machine.

## Step 1: Create a New Spring Boot Project

1. **Use Spring Initializr**:
 - Go to [Spring Initializr](https://start.spring.io/).
 - Set the project details and add the necessary dependencies (Spring Web, Spring Boot DevTools, AWS SDK S3).
 - Click **Generate** to download the project.
 - Unzip the file and open it in your IDE.

## Step 2: Add AWS SDK Dependencies

If not added during the project setup, add the following dependencies in `pom.xml`:

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
This class will configure the S3 client using credentials retrieved from Secrets Manager:
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
This class will use the S3 client to upload files to an S3 bucket:  
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
1. Start your Spring Boot application by running the main class or using your IDE’s run configuration.
2. Use a tool like Postman or curl to send a POST request:

- Method: POST
- URL: http://localhost:8080/upload
- Body: Select form-data and add the following fields:
- key: Your file key (e.g., test.txt)
- file: Choose a file to upload

```bash
curl -F "file=@path/to/your/file" http://localhost:8080/upload
```
- Click Send and verify the response: "File uploaded successfully!".
3. Verify Upload:
Check your S3 bucket via the AWS Management Console to ensure the file has been uploaded successfully.
Verify the response URL to ensure it points to the correct file in S3.
