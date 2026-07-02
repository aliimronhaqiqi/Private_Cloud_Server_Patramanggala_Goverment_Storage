# Installation Guide

## Overview

This document describes how to install the Patramanggala Cloud environment on a fresh Ubuntu Server.

The installation process covers system preparation, Docker installation, repository setup, environment configuration, and service deployment using Docker Compose.

Production configurations such as HAProxy, Tailscale, Native WAF, and Monitoring are documented separately in **Deployment.md**.

---

# System Requirements

## Minimum Requirements

- Ubuntu Server 24.04 LTS
- 2 CPU Cores
- 4 GB RAM
- 50 GB Available Storage
- Internet Connection

## Recommended Requirements

- Ubuntu Server 24.04 LTS
- 4 CPU Cores
- 8 GB RAM
- SSD for Operating System
- Dedicated HDD for Nextcloud Storage
- Static Local IP Address

---

# Prerequisites

Install the required packages.

```bash
sudo apt update
sudo apt upgrade -y

sudo apt install -y \
git \
curl \
wget \
ca-certificates \
gnupg \
lsb-release
```

---

# Install Docker Engine

Install Docker using the official repository.

```bash
curl -fsSL https://get.docker.com | sudo sh
```

Verify Docker installation.

```bash
docker --version
```

Example output:

```text
Docker version 28.x.x
```

---

# Install Docker Compose

Verify Docker Compose.

```bash
docker compose version
```

Example output:

```text
Docker Compose version v2.x.x
```

---

# Clone Repository

Clone the project repository.

```bash
git clone git@github.com:aliimronhaqiqi/Patramanggala_Cloud.git

cd Patramanggala_Cloud
```

---

# Configure Environment

Create the project environment file.

```bash
nano .env
```

Configure the required variables.

Example:

```text
MYSQL_DATABASE=nextcloud
MYSQL_USER=nextcloud
MYSQL_PASSWORD=your_password
MYSQL_ROOT_PASSWORD=your_root_password

NEXTCLOUD_VERSION=31-apache

TZ=Asia/Jakarta
```

> Adjust the values according to your deployment environment.

---

# Deploy Containers

Start all services.

```bash
docker compose up -d
```

Verify running containers.

```bash
docker ps
```

Expected services:

- MariaDB
- Redis
- Nextcloud Node 1
- Nextcloud Node 2

---

# Verify Installation

Verify Docker services.

```bash
docker compose ps
```

Check application logs.

```bash
docker compose logs
```

---

# Access Nextcloud

Open the Nextcloud web interface.

Example:

```text
http://SERVER-IP:8080
```

The login page should appear successfully.

---

# Installation Checklist

Before continuing to the deployment stage, ensure that:

- Ubuntu Server is installed.
- Docker Engine is running.
- Docker Compose is available.
- Repository has been cloned.
- Environment variables have been configured.
- Docker containers are running successfully.
- Nextcloud login page is accessible.

---

# Next Step

Continue with **Deployment.md** to configure:

- HAProxy Reverse Proxy
- High Availability
- Native WAF (HAProxy ACL)
- Tailscale VPN
- HTTPS TLS
- Uptime Kuma
- Telegram Notifications
