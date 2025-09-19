Three-Tier Web Application on AWS
🔹 Project Description
I designed and deployed a scalable, secure, and highly available Three-Tier Web Application using AWS best practices. This project demonstrates my ability to build production-like cloud architectures as a fresher exploring AWS + DevOps.

✅ Key Highlights

🏗 VPC with public & private subnets → for secure network segmentation.

🌐 Web Tier → Deployed Nginx + PHP on EC2 instances to serve dynamic content.

⚙️ Application Tier → Configured EC2 with required PHP extensions for backend processing.

🗄 Database Tier → Provisioned Amazon RDS (MySQL) with secure access & 99.9% uptime.

🔒 Security First → Used security groups & private subnets to restrict unauthorized access.

📈 Scalability → Designed architecture with the ability to scale horizontally/vertically.

📊 Architecture Diagram
<img width="917" height="1399" alt="three-tier img" src="https://github.com/user-attachments/assets/d24904de-4cc4-4a89-bdc0-6a1a7c40a76f" />
End-to-End Deployment Steps

Follow these steps to deploy the Three-Tier Web Application on AWS:

1. Setup VPC & Networking

Create a VPC (CIDR: 10.0.0.0/16).

Create 2 public subnets (for Web Tier) and 2 private subnets (for App & DB Tiers).

Attach an Internet Gateway (IGW) to the VPC.

Create NAT Gateway in the public subnet for private subnets to access the internet.

2. Security Groups & Access Control

Web Tier SG → Allow HTTP (80), HTTPS (443), and SSH (22) from your IP.

App Tier SG → Allow traffic only from Web Tier SG.

DB Tier SG → Allow traffic only from App Tier SG on port 3306 (MySQL).

3. Deploy Web Tier

Launch EC2 instances in public subnets.

Install & configure Nginx + PHP using user-data script:

#!/bin/bash
sudo yum update -y
sudo amazon-linux-extras enable php8.0
sudo yum install -y nginx php-cli php-mysqlnd
sudo systemctl enable nginx
sudo systemctl start nginx
echo "<?php phpinfo(); ?>" > /usr/share/nginx/html/index.php

4. Configure Application Tier

Launch EC2 instances in private subnets.

Install PHP extensions for backend logic (mysqli, json, curl).

Connect backend PHP to MySQL DB endpoint.

5. Setup Database Tier

Create an Amazon RDS (MySQL) instance in private subnet.

Set DB security group to allow access only from App Tier SG.

Import schema:

mysql -h <RDS-ENDPOINT> -u admin -p < schema.sql

6. Test the Application

Access Web Tier EC2 public IP / Elastic IP.

Ensure it serves dynamic content & connects to backend + DB successfully.
