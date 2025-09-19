Three-Tier Web Application on AWS

🔹 Project Description
    I designed and deployed a scalable, secure, and highly available Three-Tier Web Application using AWS best practices. This project demonstrates my ability to build production-like        cloud architectures as a fresher exploring AWS. LEMP(Linux,Nginx,Mariadb,PHP ) stack installed on System
 🎯 Project Objectives
    The main objectives of this project were to:
    Build a three-tier architecture (Web, Application, Database) following AWS best practices.Implement Secure Networking Use VPC with subnets (/24) to separate public and private            resources. Apply security groups & restricted access to control traffic flow. Deploy Scalable Web & App Tiers Host Nginx + PHP in the Web Tier (public subnet) to serve dynamic            content. Deploy backend PHP application logic in the Application Tier (private subnet).Configure a Reliable Database Layer Provision Amazon RDS (MySQL) in a private subnet.
    Ensure secure access only from the App Tier. Ensure High Availability & Uptime Design for 99.9% database uptime with Amazon RDS. Allow future scalability with Load Balancers & Auto       Scaling Groups.
    Demonstrate real-world AWS cloud skills suitable for entry-level Cloud/DevOps roles.
    Showcase ability to deploy, secure, and manage cloud infrastructure end-to-end.
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
📊 Updated Architecture with Subnets
1. Public Subnet (Web Tier server) → 10.0.1.0/24 Hosts EC2 (Nginx + PHP) Internet-facing (via IGW)
   copy form.html to /usr/share/ngnix/www/
2. Private Subnet (Application Tier server) → 10.0.2.0/24 Hosts EC2 (PHP backend) Communicates only with Web & DB tiers
   copy submit.php to /usr/share/nginx/www/
3. Private Subnet (Database Tier server) → 10.0.3.0/24 Hosts Amazon RDS (MySQL)
Accessible only from App Tier
2.   Attach an Internet Gateway (IGW) to the VPC.
   Create NAT Gateway in the public subnet for private subnets to access the internet.
3. Security Groups & Access Control
   Web Tier SG → Allow HTTP (80), HTTPS (443), and SSH (22) from your IP.
   App Tier SG → Allow traffic only from Web Tier SG.
   DB Tier SG → Allow traffic only from App Tier SG on port 3306 (MySQL).
4. Deploy Web Tier
   Launch EC2 instances in public subnets.
   Install & configure Nginx + PHP using user-data script:
   #!/bin/bash
   sudo yum update -y
   sudo amazon-linux-extras enable php8.0
   sudo yum install -y nginx php-cli php-mysqlnd
   sudo systemctl enable nginx
   sudo systemctl start nginx
   check index.php is visible or not if
   echo "<?php phpinfo(); ?>" > /usr/share/nginx/html/index.php
   now, go to the configuration path nano /etc/nginx/nginx.conf add proxy pass Add Private IP of Appserver
   <img width="2844" height="882" alt="image" src="https://github.com/user-attachments/assets/1b99d27a-d03c-4d57-a84a-c5c1fd545021" />   
5. Configure Application Tier
   Launch EC2 instances in private subnets.
   Install PHP extensions for backend logic (mysqli, json, curl).
   Connect backend PHP to MySQL DB endpoint.
6. Setup Database Tier
   Create an Amazon RDS (MySQL) instance in private subnet.
   Set DB security group to allow access only from App Tier SG.
   Import schema:
   sudo mysql -u admin -h endpoint-of-rds -p
   create database facebook;
   use facebook;
   create table users (id int not null primary key auto_increment,name varchar(50),email varchar(50),website varchar(50),comment varchar(100),gender varchar(10));
7. Test the Application
   Access Web Tier EC2 public IP.
   Ensure it serves dynamic content & connects to backend + DB successfully.
🔚 Conclusion
This project demonstrates the design and deployment of a scalable, secure, and highly available three-tier web application on AWS. By implementing best practices in networking, security, and cloud architecture, I gained valuable hands-on experience with AWS services such as VPC, EC2, RDS, and Security Groups.
