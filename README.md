# 🚀 Automated AWS Infrastructure with Terraform

This project demonstrates how to provision and manage a cloud infrastructure on **AWS** using **Terraform**. It includes the setup of a VPC, subnets, EC2 instances, RDS, S3 static website hosting, and a CI/CD pipeline with GitHub Actions—all managed as code.

---

## 📌 Features
- **Infrastructure as Code (IaC)** with Terraform
- Automated provisioning of **VPC, Subnets, EC2, RDS and S3**
- **Static Website Hosting** using **AWS S3**
- **CI/CD Pipeline** with **GitHub Actions** for automated deployments
- Modular design for enhanced reusability and clarity
- Secure configuration with Security Groups
- Terraform Outputs for easy access to resource information

---

## 🏗 Architecture
The project is organized into three main modules:

1. **Networking** – Creates the VPC, subnets, internet gateway, and routing
2. **Compute** – Launches EC2 instances for the web server
3. **Database** – Sets up an RDS instance in a private subnet
4. **Storage & Hosting** – Configures **S3** for static website hosting 

> **Note:** Instead of manually clicking through the AWS console, Terraform lets you define your entire infrastructure in code—quick, repeatable, and efficient!

---

## ⚡ Quick Start

### 🔹 Prerequisites
- **AWS CLI** installed and configured
- **Terraform** installed (version 1.3+ recommended)
- An **AWS account** (Free Tier usage is recommended)
- **GitHub Actions setup** (if using CI/CD)

### 🛠 Setup Instructions

1. **Clone the Repository**
   
   git clone https://github.com/sodbilegtb/AWS_IaC_Terraform.git
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

## 🚀 S3 Static Website Hosting
-Terraform creates an S3 bucket configured for static website hosting.
-Public access settings & bucket policy allow the website to be accessible via an S3 endpoint.

After running Terraform, your static site will be accessible via the S3 website URL provided in the outputs.

---

## 🔄 CI/CD with GitHub Actions
- A **GitHub Actions workflow** automates Terraform deployment.
- Every push to `main` triggers the CI/CD pipeline.
- The pipeline **validates**, **plans**, **applies Terraform changes**, and then **destroys the infrastructure** automatically.

### **Workflow Process**
1. **Terraform Lint & Format Check**
2. **Terraform Plan** (preview changes)
3. **Terraform Apply** (deploy changes to AWS)
4. **Terraform Destroy** (clean up resources after deployment)

> **Why does it destroy itself?**  
> This setup is useful for **temporary test environments**, ensuring that AWS resources are not left running unnecessarily. If you want a persistent infrastructure, you can modify the workflow to remove the `terraform destroy` step.

> **Location of GitHub Actions workflow file:** `.github/workflows/terraform.yml`

---

## 🛠 Future Enhancements

- Add Auto-Scaling & Load Balancers for high availability.
- Integrate a CI/CD pipeline using GitHub Actions for automated deployments.
- Implement enhanced security measures, such as IAM roles and private endpoints.

---

## 📢 Conclusion
Terraform simplifies and streamlines the process of managing AWS infrastructure—one code file, one complete infrastructure!
With the addition of S3 static website hosting and GitHub Actions CI/CD, deployments are now fully automated and scalable.
Remember to always run **terraform destroy** after tests to avoid consuming your Free Tier too quickly.

