# 🚀 Automated AWS Infrastructure with Terraform

This project demonstrates how to provision and manage a cloud infrastructure on **AWS** using **Terraform**. It includes the setup of a VPC, subnets, EC2 instances, RDS, and other AWS resources—all managed as code.

---

## 📌 Features
- **Infrastructure as Code (IaC)** with Terraform
- Automated provisioning of **VPC, Subnets, EC2, and RDS**
- Modular design for enhanced reusability and clarity
- Secure configuration with Security Groups
- Terraform Outputs for easy access to resource information

---

## 🏗 Architecture
The project is organized into three main modules:

1. **Networking** – Creates the VPC, subnets, internet gateway, and routing
2. **Compute** – Launches EC2 instances for the web server
3. **Database** – Sets up an RDS instance in a private subnet

> **Note:** Instead of manually clicking through the AWS console, Terraform lets you define your entire infrastructure in code—quick, repeatable, and efficient!

---

## ⚡ Quick Start

### 🔹 Prerequisites
- **AWS CLI** installed and configured
- **Terraform** installed (version 1.3+ recommended)
- An **AWS account** (Free Tier usage is recommended)

### 🛠 Setup Instructions

1. **Clone the Repository**
   
   git clone https://github.com/your-username/your-repository.git
   cd your-repository

2. **Initialize Terraform**

    terraform init

3. **Review the Execution Plan**

    terraform plan

4. **Apply Changes to Deploy Resources**

    terraform apply -auto-approve

5. **Display Terraform Outputs**

    terraform output

6. **Clean Up Resources After Testing**

    terraform destroy -auto-approve

---

## 🛠 Future Enhancements

- Add Auto-Scaling & Load Balancers for high availability.
- Integrate a CI/CD pipeline using GitHub Actions for automated deployments.
- Implement enhanced security measures, such as IAM roles and private endpoints.

---

## 📢 Conclusion
Terraform simplifies and streamlines the process of managing AWS infrastructure—one code file, one complete infrastructure! Remember to always run **terraform destroy** after tests to avoid consuming your Free Tier too quickly.

