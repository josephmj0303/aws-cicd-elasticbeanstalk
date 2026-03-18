# AWS CodePipeline Setup Guide

This document describes how the CI/CD pipeline is configured using AWS CodePipeline.

---

# 🚀 Overview

The pipeline automates:

* Source retrieval
* Application build
* Deployment to Elastic Beanstalk

---

# 🏗 Pipeline Architecture

```text
Bitbucket → CodePipeline → CodeBuild → Elastic Beanstalk
```

---

# 🔧 Step 1: Create Pipeline

* Go to AWS Console → CodePipeline
* Click **Create Pipeline**
* Pipeline name: `vprofile-pipeline`

---

# 🔗 Step 2: Source Stage

* Source provider: Bitbucket
* Connect repository
* Branch: `main`

---

# 🏗 Step 3: Build Stage

* Build provider: AWS CodeBuild
* Create new project:

### Configuration

* Runtime: Java 17
* Environment: Managed image
* Buildspec: Use repo `buildspec.yml`

---

# 📦 Step 4: Artifacts

* Stored in Amazon S3
* Managed automatically by CodePipeline

---

# 🚀 Step 5: Deploy Stage

* Provider: Elastic Beanstalk
* Select application and environment

---

# 🔐 IAM Roles

Ensure roles have:

* CodePipeline → access to S3, CodeBuild, EB
* CodeBuild → access to Parameter Store

---

# 🔄 Pipeline Execution Flow

1. Code commit triggers pipeline
2. Source stage pulls code
3. Build stage compiles application
4. Artifact stored in S3
5. Deploy stage updates Elastic Beanstalk

---

# 📊 Monitoring

* CodePipeline dashboard
* CodeBuild logs
* Deployment status in EB

---

# ⚠️ Common Issues

### Build failure

* Check CodeBuild logs
* Validate buildspec.yml

### Deployment failure

* Check EB events
* Verify environment health

---

# 📌 Summary

CodePipeline provides a fully managed CI/CD workflow enabling automated, repeatable deployments.

