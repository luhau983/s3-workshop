---
title: "Deploy Application EC2"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: "<b>4</b> "
---

## Deploy Spring Boot Application to EC2 and Test API

In this guide, you will learn how to deploy a Spring Boot application to an EC2 instance and test the API.


## Step 1: Launch and Configure EC2 Instance

### 1.1 Launch an EC2 Instance
![step1](/images/4.s3/ec2/step1.png)
### 1.2 Connect to Your EC2 Instance

1. **Open Terminal** on your local machine.
2. **Change Permissions** of your key pair file:
   ```bash
   chmod 400 /path/to/your-key-pair.pem
    ```
3. **Connect to EC2 Instance**:
   ```bash 
   ssh -i /path/to/your-key-pair.pem ec2-user@your-ec2-public-dns
    ```
![step2](/images/4.s3/ec2/step2.png)

## Step 2: Set Up Environment on EC1

### 2.1 Install Java and Maven
1. Install Maven:
```bash
sudo yum install java-11-openjdk -y
```
   - For Ubuntu, use:
   ```bash
   sudo apt-get update
   sudo apt-get install openjdk-11-jdk -y
   ```
2. Install Maven:
```bash
sudo yum install maven -y
```
- For Ubuntu, use:
```bash
sudo apt-get install maven -y
```
###  2.2 Transfer Your Spring Boot Application
1. **Create a JAR File** of your Spring Boot application:
   ```bash
   mvn clean package
   ```
2. **Transfer JAR File** to your EC2 instance:
   ```bash
   scp -i /path/to/your-key-pair.pem /path/to/your-spring-boot-app.jar ec2-user@your-ec2-public-dns:/home/ec2-user/
    ```
## Step 3: Run Your Spring Boot Application
### 3.1 Navigate to the Directory
1. Log in to your EC2 instance and navigate to the directory where you transferred the JAR file:
```bash
cd /home/ec2-user/
```
### 3.2 Run the JAR File
1. Run the JAR file:
```bash
java -jar your-spring-boot-app.jar
```
- You should see logs indicating that the application has started and is listening on the specified port.