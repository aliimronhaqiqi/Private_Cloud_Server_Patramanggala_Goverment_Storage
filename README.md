##

# Patramanggala Cloud

> **Private Cloud Storage Base Docker dan Nextcloud untuk Pemerintahan Desa Patramanggala**

![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04_LTS-E95420?style=for-the-badge&logo=ubuntu)
![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?style=for-the-badge&logo=docker)
![Nextcloud](https://img.shields.io/badge/Nextcloud-31-0082C9?style=for-the-badge&logo=nextcloud)
![MariaDB](https://img.shields.io/badge/MariaDB-10.11-003545?style=for-the-badge&logo=mariadb)
![Redis](https://img.shields.io/badge/Redis-7-DC382D?style=for-the-badge&logo=redis)
![HAProxy](https://img.shields.io/badge/HAProxy-Reverse_Proxy-0A4B78?style=for-the-badge)
![Tailscale](https://img.shields.io/badge/Tailscale-MagicDNS-242424?style=for-the-badge&logo=tailscale)

---

# Project Overview

Patramanggala Cloud merupakan implementasi Private Cloud Storage berbasis Nextcloud yang dirancang untuk mendukung digitalisasi administrasi Pemerintah Desa Patramanggala.

Project ini memanfaatkan Docker sebagai platform container, MariaDB sebagai database, Redis sebagai cache, HAProxy sebagai Reverse Proxy HTTPS, serta Tailscale VPN dengan MagicDNS untuk membangun akses yang aman tanpa membuka server ke internet publik.

---

# Objectives

- Membangun Private Cloud Storage.
- Menyediakan penyimpanan dokumen desa yang aman.
- Mengimplementasikan HTTPS menggunakan Tailscale Certificate.
- Menggunakan Reverse Proxy berbasis HAProxy.
- Menyiapkan implementasi Web Application Firewall (ModSecurity + OWASP CRS).

---

# System Architecture

```text
Staff
        │
        │
  Tailscale VPN
        │
 MagicDNS HTTPS
        │
     HAProxy
        │
     Nextcloud
     ├──────────┐
     │          │
   MariaDB    Redis
     │
 Storage HDD
```

---

# Technology Stack

| Component | Technology |
|-----------|------------|
| Operating System | Ubuntu Server 24.04 LTS |
| Container | Docker Compose |
| Cloud Platform | Nextcloud 31 |
| Database | MariaDB 10.11 |
| Cache | Redis 7 |
| Reverse Proxy | HAProxy |
| VPN | Tailscale |
| HTTPS | Tailscale Certificate |
| Version Control | Git + GitHub |

---

# Security Stack

- HTTPS Encryption
- Tailscale VPN
- MagicDNS
- Trusted Domains
- Trusted Proxy
- Security Headers (HSTS)
- Reverse Proxy (HAProxy)

Upcoming

- ModSecurity WAF
- OWASP Core Rule Set (CRS)

---

# Repository Structure

```text
Patramanggala_Cloud/
│
├── docker-compose.yml
├── README.md
├── .gitignore
│
├── haproxy/
│      haproxy.cfg
│
├── docs/
│
├── screenshots/
│
├── architecture/
│
└── scripts/
```

---

# Project Progress

| Milestone | Status |
|------------|---------|
| Ubuntu Server | ✅ |
| Docker Compose | ✅ |
| MariaDB | ✅ |
| Redis | ✅ |
| Nextcloud | ✅ |
| Storage HDD | ✅ |
| HTTPS | ✅ |
| HAProxy | ✅ |
| Security Headers | ✅ |
| GitHub Versioning | ✅ |
| ModSecurity | ⏳ |
| OWASP CRS | ⏳ |
| Security Testing | ⏳ |

---

# Roadmap

- [x] Ubuntu Server
- [x] Docker
- [x] MariaDB
- [x] Redis
- [x] Nextcloud
- [x] Tailscale VPN
- [x] HTTPS
- [x] HAProxy Reverse Proxy
- [ ] ModSecurity
- [ ] OWASP CRS
- [ ] Security Testing
- [ ] Backup Automation

---

# Author

**Muhamad Ali Imron Haqiqi**

Informatics Engineering
Global Institute
