
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



📌 Breakdown of Components and Their Purpose

1. Virtual Private Cloud (VPC)

Provides an isolated network environment for the infrastructure.

Ensures secure communication between components.

Allows for fine-grained control of inbound and outbound traffic.

2. Subnets

Public Subnet: Contains resources that need direct internet access (e.g., Bastion Host and Web Server).

Private Subnets: Used for internal resources like the App Server and Database, preventing direct internet access.

Multiple Availability Zones: Ensures high availability and redundancy in case of failure.

3. Internet Gateway & NAT Gateway

Internet Gateway: Enables external access to public subnet resources.

NAT Gateway: Allows instances in private subnets to access the internet for updates without exposing them to the public.

4. Security Groups

Bastion Host Security Group: Only allows SSH access from trusted sources.

Web Server Security Group: Allows HTTP/HTTPS access and SSH from the Bastion Host.

App Server Security Group: Restricts access to only Web Server instances.

Database Security Group: Allows only the App Server to communicate with the database.

5. Bastion Host (Jump Server)

Acts as a secure bridge to access private resources.

Prevents direct access to critical infrastructure from external sources.

6. Web Server

Serves the front-end and user interface.

Hosts static content and communicates with the App Server.

Runs an Apache-based web service for handling HTTP requests.

7. Application Server

Manages business logic and data processing.

Connects the Web Server with the Database.

Runs a MariaDB client to interact with the database backend.

8. Relational Database Service (RDS - MariaDB)

Stores and manages application data securely.

Allows controlled access only from the App Server.

Subnet group spans multiple Availability Zones for redundancy.

Multi-AZ Deployment: Ensures high availability by automatically replicating data across different availability zones.

Automated Backups: Provides continuous snapshots to enable point-in-time recovery.

Performance Optimization: Supports read replicas for scaling database queries efficiently.


📌 Why This Architecture Was Designed This Way

This 3-tier architecture was designed to provide:

Scalability: Each tier can be scaled independently based on demand.

Security: Public and private subnets protect sensitive resources.

High Availability: Resources are distributed across multiple Availability Zones to prevent single points of failure.

Performance Optimization: Separating the web, application, and database layers improves efficiency and reduces bottlenecks.

Cost Efficiency: By keeping critical resources private and reducing unnecessary internet exposure, operational costs are optimized.


📌 Advantages of This Architecture

Improved Security: Traffic between tiers is controlled by security groups.

Resilience & Fault Tolerance: Multi-AZ deployment ensures high availability.

Modularity: Each tier can be modified, replaced, or scaled independently.

Better Resource Management: Different layers can be optimized for their specific workloads.

Easier Maintenance & Troubleshooting: Logical separation simplifies debugging and performance monitoring.

Real-World Applications and Use Cases

1. E-commerce Platforms

Web servers handle customer interactions.

Application servers process orders and payments.

Databases store customer information and transaction records.

2. Enterprise Web Applications

Large corporations use this architecture to separate the UI, business logic, and data storage for better security and performance.

3. Online Banking & Financial Systems

Ensures secure transactions and customer data integrity.

Multi-AZ redundancy is critical for uptime and reliability.

4. Healthcare Systems

Stores and processes sensitive patient records securely.

Implements strict access controls with security groups.

5. SaaS Applications

Multi-tiered structure allows for API-based interactions between different components.

Scalable architecture supports dynamic user demand.


📌  Conclusion

This project showcases a robust 3-tier AWS architecture with security and high availability in mind.

📌 Follow my LinkedIn and Medium for more cloud projects!
💼 [LinkedIn](https://www.linkedin.com/in/roy-ivia-837055310/)| 📝 [Medium](https://medium.com/@royiviah)| 🛠️ [GitHub](https://github.com/RoyIvia)

