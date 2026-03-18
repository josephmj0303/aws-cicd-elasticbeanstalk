# AWS Elastic Beanstalk Deployment Guide

This document explains how the application is deployed using AWS Elastic Beanstalk.

---

# 🚀 Overview

AWS Elastic Beanstalk is used as the platform for deploying and managing the application.

It automatically provisions:

* EC2 instances
* Load Balancer
* Auto Scaling
* Health Monitoring

---

# 🏗 Environment Setup

## 1. Create Application

* Navigate to AWS Console → Elastic Beanstalk
* Click **Create Application**
* Application name: `vprofile-app`

---

## 2. Create Environment

* Environment type: **Web Server**
* Platform: **Tomcat (Java 17)**
* Upload application code: Use artifact from CodePipeline

---

## 3. Configure Environment

### Instance Configuration

* Instance type: `t2.micro` (for demo)
* Auto Scaling: Min 1, Max 2

---

### Load Balancer

* Application Load Balancer enabled
* Default HTTP listener (port 80)

---

### Security Groups

Ensure:

* HTTP (80) open to public
* EC2 can access RDS (port 3306)

---

# 🔐 Environment Variables

Set in:

Elastic Beanstalk → Configuration → Software → Environment Properties

---

## Required Variables

```bash
DB_URL=
DB_USERNAME=
DB_PASSWORD=

MEMCACHED_HOST=
MEMCACHED_PORT=

RABBITMQ_HOST=
RABBITMQ_PORT=
RABBITMQ_USERNAME=
RABBITMQ_PASSWORD=

ELASTIC_HOST=
ELASTIC_PORT=
ELASTIC_CLUSTER=
ELASTIC_NODE=
```

---

# 🔄 Deployment Flow

1. CodePipeline triggers deployment
2. Build artifact is pushed to Elastic Beanstalk
3. New application version is created
4. Environment updates with new version
5. Traffic routed via Load Balancer

---

# 📊 Monitoring

Use:

* Elastic Beanstalk Health Dashboard
* CloudWatch Metrics
* Logs (via EB console)

---

# ⚠️ Common Issues

### Application not starting

* Check logs under `/var/log/`
* Validate environment variables

### DB connection failure

* Verify RDS endpoint
* Check security group rules

---

# 📌 Summary

Elastic Beanstalk simplifies deployment by managing infrastructure automatically while allowing full control over application configuration.

