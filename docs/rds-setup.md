# Amazon RDS Setup Guide

This document explains how the database is configured using Amazon RDS.

---

# 🚀 Overview

Amazon RDS is used to host the MySQL database for the application.

---

# 🏗 Step 1: Create Database

* Go to AWS Console → RDS
* Click **Create Database**

---

## Configuration

* Engine: MySQL
* Version: Latest stable
* Template: Free tier (for demo)

---

## Settings

* DB instance identifier: `vprofile-db`
* Master username: `admin`
* Master password: (store in Parameter Store)

---

## Instance Configuration

* Instance class: `db.t3.micro`
* Storage: 20 GB

---

# 🌐 Step 2: Connectivity

* Public access: Disabled (recommended)
* VPC: Default or custom
* Security group:

Allow:

```bash
Port 3306 → from EC2 / EB security group
```

---

# 🔗 Step 3: Get Endpoint

After creation:

* Copy endpoint:

```bash
vprofile-db.xxxxx.us-east-1.rds.amazonaws.com
```

Store in Parameter Store:

```bash
/vprofile/db/url
```

---

# 🔐 Step 4: Security Best Practices

* Use strong passwords
* Store credentials in Parameter Store
* Restrict access via security groups
* Enable backups

---

# 🔄 Application Connection

Application connects using:

```properties
jdbc.url=${DB_URL}
jdbc.username=${DB_USERNAME}
jdbc.password=${DB_PASSWORD}
```

---

# 📊 Monitoring

* CloudWatch metrics
* RDS Performance Insights
* Logs

---

# ⚠️ Common Issues

### Connection timeout

* Check security group rules
* Verify VPC configuration

### Authentication failed

* Verify credentials in Parameter Store

---

# 📌 Summary

Amazon RDS provides a managed, scalable, and secure database solution integrated with the application via environment variables.

