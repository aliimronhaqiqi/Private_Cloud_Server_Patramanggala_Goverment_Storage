# Security

## Overview

Patramanggala Cloud implements a layered security architecture to protect village administrative data and services.

Instead of exposing the server directly to the public Internet, every connection is secured through Tailscale VPN, HTTPS encryption, HAProxy Reverse Proxy, and a lightweight Native Web Application Firewall (WAF) implemented using HAProxy Access Control Lists (ACL).

---

# Security Architecture

```text
Internet
      │
      │
Blocked
      │
──────────────
      │
Tailscale VPN
      │
HTTPS (TLS Certificate)
      │
HAProxy Reverse Proxy
      │
Native WAF (ACL)
      │
Nextcloud
      │
MariaDB
      │
Storage
```

---

# Security Layers

Patramanggala Cloud applies multiple security layers.

## Layer 1

Ubuntu Server

- Minimal server installation
- SSH access
- Linux file permissions

---

## Layer 2

Docker Isolation

Services run independently inside Docker containers.

Components include:

- MariaDB
- Redis
- Nextcloud Node 1
- Nextcloud Node 2
- HAProxy
- Uptime Kuma

---

## Layer 3

Private Network

Tailscale VPN is used to restrict access.

Benefits:

- Private network
- No public exposure
- MagicDNS
- Device authentication

---

## Layer 4

HTTPS Encryption

TLS certificates are provided by Tailscale.

Features:

- HTTPS encryption
- Secure communication
- Automatic certificate management

---

## Layer 5

HAProxy Reverse Proxy

HAProxy protects backend services by acting as the single entry point.

Functions:

- Reverse Proxy
- Load Balancer
- Health Check
- High Availability

---

## Layer 6

Native Web Application Firewall

Instead of using ModSecurity, Patramanggala Cloud implements a lightweight Native WAF using HAProxy Access Control Lists (ACL).

Implemented protections include:

- HTTP Method Filtering
- Hidden File Protection
- Sensitive Directory Protection
- Scanner Detection
- Rate Limiting
- Security Headers

---

# Implemented ACL Protection

The following attacks are mitigated:

- TRACE Method
- CONNECT Method
- SQLMap Scanner
- Nikto Scanner
- Gobuster
- DirBuster
- Masscan
- Nmap
- WPScan

Hidden resources are also protected:

- /.git
- /.env
- /.svn
- /.hg
- /backup

---

# Rate Limiting

HAProxy implements IP-based request rate limiting.

Features:

- Stick Table
- Request Tracking
- Automatic HTTP 429 Response

This mechanism helps reduce abusive requests and simple denial-of-service attempts.

---

# Security Headers

HAProxy automatically sends security-related HTTP response headers.

Implemented headers include:

- HSTS
- X-Frame-Options
- X-Content-Type-Options
- Referrer-Policy

---

# High Availability Security

HAProxy continuously monitors backend health.

If one Nextcloud node becomes unavailable:

- unhealthy node removed automatically
- traffic redirected to healthy node
- service remains accessible

This minimizes service disruption while maintaining secure access.

---

# Monitoring and Alerting

Infrastructure monitoring is implemented using Uptime Kuma.

Monitored services include:

- HAProxy
- HTTPS Endpoint
- Nextcloud Node 1
- Nextcloud Node 2

Real-time notifications are delivered through Telegram Bot whenever service status changes.

---

# Current Security Status

| Feature | Status |
|----------|:------:|
| Docker Isolation | ✅ |
| Tailscale VPN | ✅ |
| HTTPS Encryption | ✅ |
| MagicDNS | ✅ |
| Trusted Domains | ✅ |
| Trusted Proxy | ✅ |
| HAProxy Reverse Proxy | ✅ |
| High Availability | ✅ |
| Native WAF (HAProxy ACL) | ✅ |
| Rate Limiting | ✅ |
| Security Headers | ✅ |
| Uptime Kuma Monitoring | ✅ |
| Telegram Alert | ✅ |

---

# Future Improvements

The following features are planned for future releases:

- Automated Backup
- Log Aggregation
- Fail2Ban Integration
- Centralized Monitoring Dashboard

---

# Summary

Patramanggala Cloud implements a practical defense-in-depth strategy by combining private networking, encrypted communication, reverse proxy, high availability, native WAF protection, and continuous monitoring.

This architecture provides a secure, reliable, and maintainable private cloud platform for village administrative services.
