
🚀 Building a Highly Available 3-Tier Architecture on AWS 🚀

📌 Project Overview

This repository documents the implementation of a 3-Tier Highly Available Architecture on AWS, using EC2, RDS, and VPC networking.

📌 Project Scope

VPC with 4 subnets (1 public, 3 private) across 2 Availability Zones.

Security Groups to restrict access between components.

Bastion Host for secure SSH access.

Web Server serving HTTP traffic.

App Server hosting application logic.

Amazon RDS (MariaDB) as the database layer.

AWS Services Used

Networking: VPC, Subnets, Internet Gateway, NAT Gateway, Route Tables.

Compute: EC2 (Web Server, App Server, Bastion Host).

Database: Amazon RDS (MariaDB).

Security: Security Groups, Key Pairs.

📌 Setup Instructions

1️⃣ VPC & Networking

Create a VPC with CIDR 10.0.0.0/16.

Configure public and private subnets.

Set up an Internet Gateway and NAT Gateway.

Assign proper route tables to subnets.

2️⃣ Security Groups

Bastion Host SG: Allows SSH from your IP.

Web Server SG: Allows HTTP traffic from anywhere.

App Server SG: Accepts traffic from Web Server.

Database SG: Accepts traffic from App Server.

3️⃣ Instance Deployments

Bastion Host

ssh -i labsuser.pem ec2-user@bastion-host-public-ip

Web Server (Apache)

#!/bin/bash
sudo yum update -y
sudo amazon-linux-extras enable php7.2
sudo yum install -y httpd php
sudo systemctl start httpd
sudo systemctl enable httpd

App Server (MariaDB Client)

#!/bin/bash
sudo yum install -y mariadb-server
sudo systemctl start mariadb

4️⃣ Database Setup (RDS)

Create an RDS Subnet Group.

Configure an Amazon RDS (MariaDB) instance.

Disable automated backups & encryption for simplicity.

5️⃣ Connecting via Bastion Host

Upload SSH keys and connect securely.

scp -i labsuser.pem labsuser.pem ec2-user@bastion-host-public-ip:/home/ec2-user
ssh -i labsuser.pem ec2-user@app-server-private-ip
mysql --user=root --password='Re:Start!9' --host=database-server-endpoint

📌 Testing & Validation

Ping Web Server from App Server.

Access Apache Server via Public IP.

Verify Database Connection from App Server.

Conclusion

This project showcases a robust 3-tier AWS architecture with security and high availability in mind.

📌 Follow my LinkedIn and Medium for more cloud projects!
💼 [LinkedIn](https://www.linkedin.com/in/roy-ivia-837055310/)| 📝 [Medium](https://medium.com/@royiviah)| 🛠️ [GitHub](https://github.com/RoyIvia)

