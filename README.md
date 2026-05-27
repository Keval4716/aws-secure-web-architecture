# AWS Secure Web Hosting Architecture

## Project Overview
This project demonstrates how to deploy a secure web infrastructure on AWS using foundational cloud services. It is designed to host a website while maintaining strict network isolation and security controls.

## Services Used
* **Amazon VPC:** Custom network isolation with Public and Private subnets.
* **Amazon EC2:** Linux-based virtual server configured as an Apache web server.
* **Amazon S3:** Private storage bucket hosting static web application assets.
* **AWS IAM:** Secure instance profiles ensuring credential-less service access.

## Architecture & Implementation Steps

### 1. Network Isolation (VPC)
I built a custom VPC with a dedicated Public Subnet for the web traffic and a Private Subnet for secure backend assets. 
* *Insert VPC Screenshot below:*
![VPC Configuration](vpc.png)

### 2. Linux Server & Web Configuration
Launched an Amazon Linux EC2 instance. Connected via SSH, updated the package manager, installed Apache, and successfully verified that the server could process HTTP traffic.
* *Insert Terminal/Webpage Screenshot below:*
![Live Web Server](linux.png)

### 3. Security Hardening (IAM & Security Groups)
Configured inbound Security Group rules to strictly restrict traffic (allowing HTTP port 80 globally and locking down SSH port 22). Attached an IAM role to the instance profile to securely pull deployment assets directly from a private S3 bucket.
* *Insert IAM/Security Group Screenshot below:*
![Security Groups](security.png)
