# Deployment Guide

## Overview

This document describes the deployment process of Patramanggala Cloud after the base installation has been completed.

The deployment includes configuring a High Availability architecture using two Nextcloud application nodes, HAProxy Reverse Proxy, Native Web Application Firewall (ACL), Tailscale VPN, HTTPS, and infrastructure monitoring with Uptime Kuma.

---

# Deployment Architecture

The deployed infrastructure consists of the following services:

- MariaDB Database
- Redis Cache
- Nextcloud Node 1
- Nextcloud Node 2
- HAProxy Reverse Proxy
- Native WAF (HAProxy ACL)
- Tailscale VPN
- HTTPS (Tailscale TLS Certificate)
- Uptime Kuma Monitoring
- Telegram Notification

---

# Deployment Workflow

```text
Ubuntu Server
      │
Docker Compose
      │
MariaDB + Redis
      │
Nextcloud Node 1
      │
Nextcloud Node 2
      │
HAProxy Reverse Proxy
      │
Native WAF (ACL)
      │
Tailscale VPN
      │
HTTPS TLS
      │
Uptime Kuma
      │
Telegram Notification
```

---

# Deploy Database

Start the database service.

```bash
docker compose up -d db
```

Verify the database container.

```bash
docker ps
```

---

# Deploy Redis

Start Redis.

```bash
docker compose up -d redis
```

Verify Redis.

```bash
docker ps
```

---

# Deploy Nextcloud Nodes

Deploy both application nodes.

```bash
docker compose up -d app
docker compose up -d app2
```

Verify:

```bash
docker ps
```

Expected:

- Nextcloud Node 1
- Nextcloud Node 2

---

# Configure HAProxy

Deploy HAProxy.

```bash
docker compose up -d haproxy
```

HAProxy provides:

- Reverse Proxy
- Load Balancing
- Health Check
- HTTPS Termination

---

# Configure Round Robin

Traffic distribution uses the Round Robin algorithm.

```text
Client Request

↓

HAProxy

↓

Node 1

↓

Node 2

↓

Node 1

↓

Node 2
```

This mechanism distributes client requests evenly between both application nodes.

---

# Health Check

HAProxy periodically checks backend availability.

If one backend becomes unavailable:

- unhealthy node removed automatically
- traffic redirected to healthy node
- users continue accessing the service

No manual intervention is required.

---

# Native Web Application Firewall

Patramanggala Cloud implements a lightweight Native WAF using HAProxy Access Control Lists (ACL).

Implemented protections include:

- HTTP Method Filtering
- Hidden File Protection
- Sensitive Directory Protection
- Scanner Detection
- Rate Limiting
- Security Headers

---

# Configure Tailscale VPN

Authenticate the server.

```bash
sudo tailscale up
```

Verify.

```bash
tailscale status
```

---

# Configure HTTPS

HTTPS is enabled using Tailscale TLS Certificates.

Verify.

```text
https://<tailscale-hostname>
```

---

# Infrastructure Monitoring

Monitoring is implemented using Uptime Kuma.

Configured monitors:

- HAProxy
- HTTPS Endpoint
- Nextcloud Node 1
- Nextcloud Node 2

---

# Telegram Notification

Telegram Bot is configured to receive infrastructure alerts.

Notification events:

- Service Down
- Service Recovery

This allows administrators to receive real-time infrastructure status updates.

---

# Deployment Verification

The deployment is considered successful when:

- All Docker containers are running.
- HAProxy is accessible.
- HTTPS is working.
- Both Nextcloud nodes are healthy.
- Round Robin load balancing is operational.
- Failover works correctly.
- Native WAF is active.
- Uptime Kuma reports all services as UP.
- Telegram notifications are delivered successfully.

---

# Next Step

Continue with **Security.md** to understand the security architecture implemented in Patramanggala Cloud.
