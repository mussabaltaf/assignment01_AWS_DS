# 🎓 UniEvent: Scalable University Event Management System
### Cloud Architecture Design | AWS Deployment | CE 308/408 Cloud Computing

![AWS Architecture](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Infrastructure](https://img.shields.io/badge/Infrastructure-High--Availability-green?style=for-the-badge)
![Security](https://img.shields.io/badge/Security-Private--Subnet-blue?style=for-the-badge)

## 📌 Project Overview
**UniEvent** is a centralized, cloud-hosted platform designed for university students to browse events, register for activities, and manage event-related media. 

The system is architected to be **secure, scalable, and fault-tolerant**, ensuring 100% availability even during peak registration periods (e.g., society recruitment drives or annual festivals). It features automated data ingestion from external Open APIs to keep the event feed updated without manual entry.

---

## 🏗️ Architectural Blueprint
The system follows AWS Best Practices by decoupling the web tier from the public internet and utilizing managed services for high availability.

### 🛡️ Networking & Security (VPC & IAM)
* **Custom VPC:** A dedicated Virtual Private Cloud with two **Public Subnets** and two **Private Subnets** across multiple Availability Zones (AZs).
* **Isolation:** The Application logic (EC2) resides in **Private Subnets**, making them invisible to the public internet.
* **NAT Gateway:** Enables private EC2 instances to fetch external API data securely without exposing them to inbound threats.
* **IAM Roles:** Implemented the *Principle of Least Privilege* by using IAM roles for EC2-to-S3 communication, eliminating the need for hardcoded credentials.

### ⚡ Compute & Scaling (EC2 & ELB)
* **Elastic Load Balancer (ALB):** Acts as the entry point in the public subnet, distributing student traffic across multiple EC2 instances.
* **Fault Tolerance:** If an instance in one AZ fails, the ALB automatically reroutes traffic to healthy instances in other AZs (Zero Downtime).
* **Automated Ingestion:** A background process periodically fetches structured JSON data from the **Ticketmaster Discovery API**.

### 📦 Storage (Amazon S3)
* **Persistent Metadata:** Event details fetched from the API are stored as JSON objects in S3.
* **Media Assets:** Event posters and images are stored securely in an S3 bucket with restricted access policies.

---

## 🛠️ Tech Stack & AWS Services
| Service | Purpose |
| :--- | :--- |
| **VPC** | Logical isolation of the university network environment. |
| **EC2** | Hosting the UniEvent web application on Linux instances. |
| **ELB** | Ensuring high availability and traffic distribution. |
| **S3** | Secure storage for event JSON data and media/posters. |
| **IAM** | Managing secure access between AWS resources. |
| **NAT Gateway** | Providing outbound internet access for private instances. |

---

## 🚀 Deployment Steps (Logical Flow)
1. **Network Setup:** Create VPC, Subnets, and Route Tables. Attach an Internet Gateway (IGW) to the public subnets.
2. **Compute Layer:** Provision EC2 instances using an Amazon Linux AMI within the private subnets.
3. **Load Balancing:** Deploy an Application Load Balancer in the public subnets and register EC2 instances in a Target Group.
4. **Data Integration:** Configure the application to fetch data from the chosen API and upload assets to S3 using an IAM Instance Profile.
5. **Security Hardening:** Configure Security Groups to only allow traffic into EC2 from the Load Balancer's Security Group (Port 80/443).

---

## 👤 Author
**M. Mussab Altaf** *Computer Science Student* *Ghulam Ishaq Khan Institute (GIKI)*

---
*This project was developed as part of the CE 308/408 Cloud Computing course.*
<img width="2395" height="824" alt="image" src="https://github.com/user-attachments/assets/e6b4daaa-4d26-45a4-baf7-433dc2af4f93" />
<img width="2879" height="1314" alt="image" src="https://github.com/user-attachments/assets/0bce69eb-04f6-4954-8652-aac081ad8c53" />
<img width="2879" height="794" alt="image" src="https://github.com/user-attachments/assets/4e44d606-7bda-46ba-a5dc-07827e03799d" />



