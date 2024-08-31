---
title: "Deploy Application EC2"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: "<b>4</b> "
---

## Deploy Spring Boot Application to EC2 and Test API

In this guide, you will learn how to deploy a Spring Boot application to an EC2 instance and test the API.


## Bước 1: Khởi Tạo và Cấu Hình EC2 Instance

### 1.1  Khởi Tạo Một EC2 Instance
![step1](/images/4.s3/ec2/step1.png)
### 1.2 Kết Nối Với EC2 Instance

1. **Mở Terminal** trên máy tính của bạn.
2. **Change Permissions** key pair file:
   ```bash
   chmod 400 /path/to/your-key-pair.pem
    ```
3. **Kết Nối EC2 Instance**:
   ```bash 
   ssh -i /path/to/your-key-pair.pem ec2-user@your-ec2-public-dns
    ```
![step2](/images/4.s3/ec2/step2.png)

## Bước 2: Cài Đặt Môi Trường trên EC2

### 2.1  Cài Đặt Java và Maven
1. Cài Đặt Java:
```bash
sudo yum install java-11-openjdk -y
```
- Đối với Ubuntu, sử dụng:
   ```bash
   sudo apt-get update
   sudo apt-get install openjdk-11-jdk -y
   ```
2. Cài Đặt Maven:
```bash
sudo yum install maven -y
```
- Đối với Ubuntu, sử dụng:
```bash
sudo apt-get install maven -y
```
###  2.2 Chuyển Ứng Dụng Spring Boot của Bạn
1. **Create a JAR File** của ứng dụng Spring Boot của bạn:
   ```bash
   mvn clean package
   ```
2. **Chuyển Tệp JAR** lên EC2 instance của bạn:
   ```bash
   scp -i /path/to/your-key-pair.pem /path/to/your-spring-boot-app.jar ec2-user@your-ec2-public-dns:/home/ec2-user/
    ```
## Step 3: Chạy Ứng Dụng Spring Boot
### 3.1 Di Chuyển Đến Thư Mục
1. Đăng nhập vào EC2 instance của bạn và di chuyển đến thư mục nơi bạn đã chuyển tệp JAR
```bash
cd /home/ec2-user/
```
### 3.2 Chạy Tệp JAR
1. Chạy tệp JAR
```bash
java -jar your-spring-boot-app.jar
```
- Bạn sẽ thấy các log cho biết rằng ứng dụng đã bắt đầu và đang listen trên port được chỉ định.