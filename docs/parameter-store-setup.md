# AWS Parameter Store & Environment Configuration

This document describes how application secrets and configuration values are managed securely using AWS Systems Manager Parameter Store and Elastic Beanstalk environment variables.

---

# 🔐 Why Parameter Store?

In this project, sensitive data such as database credentials and service endpoints are **not stored in the source code**.

Instead, we use:

* AWS Systems Manager Parameter Store
* IAM-based secure access
* Runtime injection into the application

This ensures:

* No secrets in Git repositories
* Secure CI/CD pipelines
* Environment-specific configuration

---

# 📦 Parameter Store Keys

Create the following parameters in:

AWS Console → Systems Manager → Parameter Store

---

## Database Configuration

```bash
/vprofile/db/url
/vprofile/db/username
/vprofile/db/password
```

---

## Memcached Configuration

```bash
/vprofile/memcached/host
/vprofile/memcached/port
/vprofile/memcached/standby-host
/vprofile/memcached/standby-port
```

---

## RabbitMQ Configuration

```bash
/vprofile/rabbitmq/host
/vprofile/rabbitmq/port
/vprofile/rabbitmq/username
/vprofile/rabbitmq/password
```

---

## Elasticsearch Configuration

```bash
/vprofile/elasticsearch/host
/vprofile/elasticsearch/port
/vprofile/elasticsearch/cluster
/vprofile/elasticsearch/node
```

---

# ⚠️ Parameter Types

| Parameter | Type         |
| --------- | ------------ |
| username  | String       |
| password  | SecureString |
| endpoints | String       |

---

# 🔧 CodeBuild Integration

The pipeline retrieves these parameters using `buildspec.yml`:

```yaml
env:
  parameter-store:
    DB_USERNAME: "/vprofile/db/username"
    DB_PASSWORD: "/vprofile/db/password"
```

These values are injected as environment variables during the build.

---

# 🚀 Elastic Beanstalk Configuration

The application runs on Elastic Beanstalk and requires the same environment variables.

Configure them here:

Elastic Beanstalk → Environment → Configuration → Software → Environment Properties

---

## Required Environment Variables

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

# 🔄 Configuration Flow

```text
Parameter Store
      │
      ▼
AWS CodeBuild (CI)
      │
      ▼
Elastic Beanstalk (Runtime)
      │
      ▼
Application (reads via environment variables)
```

---

# 🔒 Security Best Practices

* Do not store secrets in Git
* Use SecureString for sensitive values
* Restrict IAM access to Parameter Store
* Rotate credentials regularly

---

# 📌 Summary

This setup ensures:

* Secure secret management
* Clean separation of code and configuration
* Production-ready CI/CD pipeline

