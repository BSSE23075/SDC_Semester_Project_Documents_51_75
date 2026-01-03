# Cloud-Native Hostel Management System ☁️🏨

![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Flask](https://img.shields.io/badge/flask-%23000.svg?style=for-the-badge&logo=flask&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)

A modernized, containerized web application designed to streamline student record management and room allocation. This project migrates a legacy monolithic architecture to a **Serverless AWS Fargate** environment, ensuring high availability, auto-scaling, and secure data persistence.

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Architecture](#-architecture)
- [Key Features](#-key-features)
- [Technology Stack](#-technology-stack)
- [Prerequisites](#-prerequisites)
- [Installation & Local Setup](#-installation--local-setup)
- [Deployment (GitOps)](#-deployment-gitops)
- [Team](#-team)

---

## 🚀 Project Overview

Traditional hostel management systems often suffer from single points of failure, lack of scalability, and data loss risks. This project solves these issues by deploying a **Flask-based application** on **AWS ECS (Fargate)**.

**Core Objectives:**

* **Decouple Infrastructure:** Eliminate manual server management using Serverless Containers.
* **Persistence:** Solve ephemeral container storage issues by integrating **Amazon S3** (media) and **Amazon RDS** (data).
* **Security:** Isolate the database in private subnets and implement OTP authentication.
* **Automation:** Zero-downtime deployments via **GitHub Actions**.

---

## 🏗 Architecture

The system is deployed across **Multi-Availability Zones (Multi-AZ)** for fault tolerance.

* **Public Subnets:** Host the Application Load Balancer (ALB).
* **Private Subnets:** Host the Fargate Tasks (App) and RDS (Database).
* **Storage:** S3 Buckets for static assets (images).

![Architecture Diagram](./assets/architecture-diagram.png)
*(Note: Upload your architecture diagram to an 'assets' folder and update this link)*

---

## ✨ Key Features

* **Auto-Scaling Infrastructure:** Automatically adjusts compute resources based on traffic via AWS Fargate.
* **Secure Authentication:** OTP (One-Time Password) logic implemented via SMTP/Amazon SES to prevent unauthorized access.
* **Cloud-Native Persistence:**
  * Student profiles/images stored in **Amazon S3**.
  * Relational data stored in a private **Amazon RDS (MySQL)** instance.
* **Bulk Data Processing:** Administrative feature to upload bulk student records via Excel.
* **Financial Dashboard:** Real-time visualization of Income vs. Expenses.
* **Zero-Downtime Deployment:** Automated CI/CD pipeline updates the application without taking the service offline.

---

## 🛠 Technology Stack


| Layer                | Technology                       |
| :------------------- | :------------------------------- |
| **Backend**          | Python 3.11, Flask Framework     |
| **Frontend**         | HTML5, Bootstrap 5, Particles.js |
| **Containerization** | Docker                           |
| **Orchestration**    | AWS ECS (Fargate)                |
| **Database**         | Amazon RDS (MySQL 8.0)           |
| **Storage**          | Amazon S3                        |
| **CI/CD**            | GitHub Actions                   |
| **Infrastructure**   | VPC, ALB, Security Groups, IAM   |

---

## 📋 Prerequisites

Before running the project, ensure you have the following:

* **Docker Desktop** installed.
* **Python 3.11+** installed.
* **AWS Account** with permissions for ECS, ECR, RDS, and S3.
* **AWS CLI** configured locally.

---

## 💻 Installation & Local Setup

1. **Clone the Repository**

   ```bash
   git clone https://github.com/your-username/hostel-management-system.git
   cd hostel-management-system
   ```
2. **Set up Virtual Environment**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. **Install Dependencies**

   ```bash
   pip install -r requirements.txt
   ```
4. **Configure Environment Variables**
   Create a `.env` file in the root directory:

   ```env
   DB_HOST=your-rds-endpoint-or-localhost
   DB_USER=admin
   DB_PASSWORD=yourpassword
   DB_NAME=hostel_db
   AWS_ACCESS_KEY_ID=your_key
   AWS_SECRET_ACCESS_KEY=your_secret
   S3_BUCKET=your-bucket-name
   SECRET_KEY=your_flask_secret_key
   ```
5. **Run Locally**

   ```bash
   flask run
   ```

---

## 🔄 Deployment (GitOps)

This repository uses **GitHub Actions** for Continuous Deployment.

**Workflow File:** `.github/workflows/deploy.yml`

**Steps:**

1. **Push:** Code is pushed to the `main` branch.
2. **Build:** GitHub Runner builds the Docker image.
3. **Push to ECR:** Image is tagged and pushed to Amazon Elastic Container Registry.
4. **Deploy to ECS:** The service is updated with the new image tag, forcing a rolling update in Fargate.

To enable this, add the following **Secrets** to your GitHub Repository settings:

* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`
* `AWS_REGION`
* `ECR_REPOSITORY`

## 👥 Team

**Institution:** Information Technology University (ITU)
**Supervisors:** Dr. Zunnurain Hussain & Sir Umair Makhdoom


| Name               | ID        | Role                        |
| :----------------- | :-------- | :-------------------------- |
| **Asma Haider**    | BSSE23051 | Cloud Architecture & DevOps |
| **Uzair Abdullah** | BSSE23075 | Backend Development & DB    |

---

*© 2026 Cloud-Native Hostel Management System*
