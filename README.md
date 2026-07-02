# Rancang Bangun Private Cloud Server Base on Docker Terintegrasi Web Aplication Firewall (WAF) & HAProxy.

> **High Availability Private Cloud Storage for Patramanggala Village Government using Nextcloud, Docker, HAProxy, Native WAF, and Tailscale VPN**

![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04_LTS-E95420?style=for-the-badge&logo=ubuntu)
![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?style=for-the-badge&logo=docker)
![Nextcloud](https://img.shields.io/badge/Nextcloud-31-0082C9?style=for-the-badge&logo=nextcloud)
![MariaDB](https://img.shields.io/badge/MariaDB-10.11-003545?style=for-the-badge&logo=mariadb)
![Redis](https://img.shields.io/badge/Redis-7-DC382D?style=for-the-badge&logo=redis)
![HAProxy](https://img.shields.io/badge/HAProxy-Load_Balancer-0A4B78?style=for-the-badge)
![Tailscale](https://img.shields.io/badge/Tailscale-MagicDNS-242424?style=for-the-badge&logo=tailscale)
![Uptime Kuma](https://img.shields.io/badge/Uptime-Kuma-5CDD8B?style=for-the-badge)

---

# Project Overview

Patramanggala Cloud is a High Availability Private Cloud infrastructure developed for the Patramanggala Village Government using Nextcloud as the collaboration platform.

The infrastructure is designed with High Availability, secure remote access through Tailscale VPN, HTTPS encryption, HAProxy Reverse Proxy & Load Balancer, Native Web Application Firewall (ACL), centralized monitoring using Uptime Kuma, and Telegram notification.

The objective is to provide a secure, reliable, maintainable, and lightweight private cloud solution without exposing services directly to the public Internet.

---

# Features

- High Availability Nextcloud Cluster
- Dual Nextcloud Application Nodes
- HAProxy Reverse Proxy
- Round Robin Load Balancing
- Automatic Health Check
- Automatic Failover
- Native Web Application Firewall (HAProxy ACL)
- HTTPS using Tailscale TLS Certificate
- Redis Cache
- MariaDB Database
- Docker Compose Deployment
- Uptime Kuma Monitoring
- Telegram Notification
- Git Versioning

---

# Objectives

- Build a private cloud storage platform.
- Secure document storage for village administration.
- Implement High Availability architecture.
- Secure communication using HTTPS.
- Deploy HAProxy as Reverse Proxy and Load Balancer.
- Implement lightweight Native WAF using HAProxy ACL.
- Monitor infrastructure health in real time.
- Send automatic notifications via Telegram.

---

# System Architecture

```text
                        Users

                          │

                   Tailscale VPN

                          │

                  HTTPS (TLS)

                          │

         HAProxy Reverse Proxy + Native WAF

                Round Robin Load Balancer

               ┌────────────────────────┐
               │                        │

      Nextcloud Node 1          Nextcloud Node 2

               │                        │
               └──────────┬─────────────┘

                      MariaDB

                         │

                      Redis

                         │

                   Storage HDD

                         │

                  Uptime Kuma

                         │

             Telegram Notification
```

---

# Technology Stack

| Component | Technology |
|------------|------------|
| Operating System | Ubuntu Server 24.04 LTS |
| Container Platform | Docker Compose |
| Cloud Platform | Nextcloud 31 |
| Database | MariaDB 10.11 |
| Cache | Redis 7 |
| Reverse Proxy | HAProxy |
| Load Balancer | HAProxy Round Robin |
| Native WAF | HAProxy ACL |
| VPN | Tailscale |
| HTTPS | Tailscale TLS Certificate |
| Monitoring | Uptime Kuma |
| Notification | Telegram Bot |
| Version Control | Git & GitHub |

---

# Repository Structure

```text
Patramanggala_Cloud/

├── architecture/
├── backup/
├── docs/
├── haproxy/
├── screenshots/
├── scripts/
├── services/
│   ├── demo/
│   └── monitoring/
├── waf/
│   ├── acl/
│   ├── tests/
│   └── README.md
│
├── docker-compose.yml
├── CHANGELOG.md
├── LICENSE
├── README.md
└── .gitignore
```

---

# High Availability

The infrastructure implements High Availability using two Nextcloud application nodes behind HAProxy.

### Features

- Round Robin Load Balancing
- Automatic Health Check
- Automatic Failover
- Shared Storage
- Zero Manual Intervention

---

# Monitoring

Infrastructure monitoring is implemented using **Uptime Kuma**.

### Monitored Services

- HAProxy
- Nextcloud HTTPS
- Nextcloud Node 1
- Nextcloud Node 2
- MariaDB
- Redis
- VPN Connectivity

### Notification Channel

- Telegram Bot

---

# Native Web Application Firewall

Instead of deploying ModSecurity, this project implements a lightweight Web Application Firewall using **HAProxy ACL**.

### Implemented Protection

- Rate Limiting
- Hidden File Protection
- Sensitive Directory Blocking
- TRACE Method Blocking
- CONNECT Method Blocking
- Scanner Detection
- HTTP Security Headers

---

# Security Features

- HTTPS Encryption
- Tailscale VPN
- MagicDNS
- Trusted Domains
- Trusted Proxy
- HAProxy Native ACL Firewall
- Security Headers (HSTS)
- X-Frame-Options
- X-Content-Type-Options
- Referrer Policy
- Permissions Policy
- Request Rate Limiting

---

# Project Progress

| Milestone | Status |
|------------|---------|
| Ubuntu Server | ✅ |
| Docker Compose | ✅ |
| MariaDB | ✅ |
| Redis | ✅ |
| Nextcloud Node 1 | ✅ |
| Nextcloud Node 2 | ✅ |
| Shared Storage | ✅ |
| HAProxy Reverse Proxy | ✅ |
| Round Robin Load Balancer | ✅ |
| Automatic Failover | ✅ |
| Native WAF (ACL) | ✅ |
| HTTPS (Tailscale TLS) | ✅ |
| Uptime Kuma Monitoring | ✅ |
| Telegram Notification | ✅ |
| Security Headers | ✅ |
| GitHub Versioning | ✅ |
| Backup Automation | ⏳ |
| Security Testing | ⏳ |

---

# Roadmap

- [x] Ubuntu Server
- [x] Docker Compose
- [x] MariaDB
- [x] Redis
- [x] Nextcloud Cluster
- [x] HAProxy Reverse Proxy
- [x] Round Robin Load Balancer
- [x] Automatic Failover
- [x] Native WAF
- [x] HTTPS (Tailscale TLS)
- [x] Uptime Kuma Monitoring
- [x] Telegram Notification
- [ ] Backup Automation
- [ ] Security Testing
- [ ] Production Release v1.0

---

# Documentation

Detailed technical documentation is available in the **docs** directory.

- Architecture
- Installation
- Deployment
- Security
- Backup
- Troubleshooting

---

# Future Improvements

- Automated Backup
- Prometheus Integration
- Grafana Dashboard
- Centralized Logging
- Email Notification
- Multi-site Replication

---

# Screenshots

> Screenshots will be added after the production release.

- Login Page
- Nextcloud Dashboard
- HAProxy Statistics
- Uptime Kuma Dashboard
- Telegram Notifications
- Native WAF Testing
- Failover Demonstration

---

# Author

**PROJECT-2**

Bachelor of Informatics Engineering

Global Institute Technology & Bussiness

---

# License

This project is licensed under the MIT License.
