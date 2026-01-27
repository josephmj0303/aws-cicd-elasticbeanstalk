# AWS CI/CD Project – Elastic Beanstalk Deployment

## 📌 Overview
This project demonstrates a complete **AWS CI/CD pipeline** for deploying a Java-based web application using **AWS native DevOps services**.

The **application source code is maintained in Bitbucket**, while this repository focuses on:
- CI/CD pipeline design
- Build automation
- Artifact management
- Automated deployment
- Production-ready AWS architecture

---

## 🏗 Architecture Overview

![AWS CI/CD Architecture](architecture/aws-ci-cd-architecture.png)

### CI Flow
![Continuous Integration](architecture/continuous-integration.png)

### CD Flow
![Continuous Delivery](architecture/continuous-delivery.png)

---

## 🔁 CI/CD Pipeline Flow

1. **Developer commits code** to Bitbucket
2. **AWS CodePipeline** detects changes
3. **AWS CodeBuild (Build Stage)**  
   - Builds application  
   - Publishes artifact to S3  
4. **AWS Elastic Beanstalk**  
   - Pulls artifact from S3  
   - Deploys application
5. **Amazon RDS**  
   - Backend database

---

## 🧰 AWS Services Used

| Service | Purpose |
|------|--------|
| AWS CodePipeline | Orchestrates CI/CD workflow |
| AWS CodeBuild | Build & test automation |
| AWS Elastic Beanstalk | Application deployment |
| Amazon S3 | Artifact storage |
| Amazon RDS | Application database |
| AWS IAM | Secure access control |

---

## 📦 Repository Structure

```
aws-ci-cd-elastic-beanstalk/
├── README.md
├── architecture/
│   ├── aws-ci-cd-architecture.png
│   ├── continuous-integration.png
│   ├── continuous-delivery.png
│
├── pipeline/
│   ├── buildspec.yml
│   ├── codepipeline-config.md
│
├── elastic-beanstalk/
│   ├── environment-config.md
│   ├── deployment-strategy.md
│
├── screenshots/
│   ├── codepipeline-success.png
│   ├── codebuild-success.png
│   ├── elastic-beanstalk-home.png
│   ├── elastic-beanstalk-login.png
│
└── docs/
    ├── services-used.md
    ├── security-and-iam.md
    ├── cost-and-free-tier.md
```
---

📸 Pipeline Execution Evidence

CodePipeline – Successful Execution

Elastic Beanstalk – Application Home

Elastic Beanstalk – Login Page

---

🔐 Security & IAM

* IAM roles with least privilege

* CodePipeline service role

* CodeBuild execution role

* Elastic Beanstalk EC2 role

Details: docs/security-and-iam.md

---

💰 Cost Considerations

 * Uses AWS Free Tier

* Elastic Beanstalk → EC2 t2.micro

* RDS → db.t3.micro

* S3 storage minimal

* CodePipeline free for first pipeline

Details: docs/cost-and-free-tier.md

---

🧠 Key DevOps Concepts Demonstrated

* CI/CD automation

* Artifact management

* Infrastructure abstraction

* Production-style deployment

---

📌 Note

This repository contains only DevOps artifacts.

Application source code is maintained securely in Bitbucket.
