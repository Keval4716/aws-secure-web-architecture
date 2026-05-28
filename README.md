# Secure AWS Web Application Deployment Pipeline

A robust cloud infrastructure project demonstrating how to architect a custom network and securely deploy a public-facing web application on an Amazon EC2 instance. The architecture enforces security best practices by using an IAM instance profile to dynamically retrieve web assets from Amazon S3 without embedding hardcoded credentials.

---

## 🛠️ Key Architectural Features Built
* **Custom VPC Architecture:** Isolated virtual network featuring public and private subnets, customized route tables, and an attached Internet Gateway for structured ingress/egress.
* **IAM Least Privilege Access:** Avoided insecure credential storage by creating a dedicated IAM service role (`EC2-S3-Read-Role`) allowing read-only access to specific S3 assets.
* **Secured Web Tier (Apache):** Provisioned an EC2 host running Amazon Linux 2023, bootstrapped with an Apache HTTP web server configured to serve custom code.
* **Dynamic Content Syncing:** Utilized the AWS CLI seamlessly within the host environment to pull live assets down from a secure S3 bucket directly into production.

---

## 📸 Step-by-Step Implementation Evidence

### 1. Secure Asset Storage & Access Control
We initialized a centralized Amazon S3 bucket to store web components securely, paired with a custom IAM Instance Profile role to allow the web server to access it automatically.
<p align="center">
  <img src="screenshots/1-S3-Bucket.jpg" width="45%" />
  <img src="screenshots/2-IAM-Role.jpg" width="45%" />
</p>

---

### 2. Custom Network Topology & Compute Provisioning
 A complete Virtual Private Cloud (VPC) was constructed from scratch, routing traffic clearly through a public gateway. An EC2 computing host was then targeted and deployed into the public zone.
<p align="center">
  <img src="screenshots/3-Custom-VPC.jpg" width="45%" />
  <img src="screenshots/4-Running-EC2.jpg" width="45%" />
</p>

---

### 3. Server Configuration & Production Launch
We accessed the infrastructure via an SSH terminal shell to initialize the web engine, seamlessly pull our `index.html` layout along with high-res assets down via the S3 pipeline, and bring the live site completely online.
<p align="center">
  <img src="screenshots/5-S3-Copy-Success.jpg" width="45%" />
  <img src="screenshots/6-Webpage-Complete.jpg" width="45%" />
</p>

---

## 🚀 Terminal Deployment Commands Used
```bash
# 1. Elevate privileges and install Apache Web Engine
sudo dnf install -y httpd

# 2. Activate the service and ensure persistence across host reboots
sudo systemctl start httpd
sudo systemctl enable httpd

# 3. Securely synchronize production assets down from S3 Bucket
sudo aws s3 cp s3://keval-s3-demo-bucket/index.html /var/www/html/index.html
sudo aws s3 cp s3://keval-s3-demo-bucket/jeams\ lee.webp /var/www/html/jeams\ lee.webp
sudo aws s3 cp s3://keval-s3-demo-bucket/kite.webp /var/www/html/kite.webp
