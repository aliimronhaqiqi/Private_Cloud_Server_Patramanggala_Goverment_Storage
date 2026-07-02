# System Architecture

## Components

- Ubuntu Server 24.04 LTS
- Docker Compose
- Nextcloud Node 1
- Nextcloud Node 2
- MariaDB
- Redis
- HAProxy Reverse Proxy
- Native WAF (HAProxy ACL)
- Tailscale VPN
- HTTPS (Tailscale TLS Certificate)
- Uptime Kuma
- Telegram Bot
---

## Architecture Diagram

                           Staff Device
                                │
                         Tailscale VPN
                                │
                       HTTPS (MagicDNS)
                                │
          HAProxy Reverse Proxy + Native WAF
                                │
                  Round Robin Load Balancer
                    ┌─────────────────────┐
                    │                     │
          Nextcloud Node 1      Nextcloud Node 2
                    │                     │
                    └──────────┬──────────┘
                               │
          ┌────────────────────┼────────────────────┐
          │                    │                    │
      MariaDB              Redis             Storage HDD

                               │
                         Uptime Kuma
                               │
                    Telegram Notification

---

## Data Flow

User
   │
Tailscale VPN
   │
HTTPS
   │
HAProxy
   │
Round Robin
   │
Nextcloud Node 1 / Node 2
   │
MariaDB
   │
Redis
   │
Storage
---

## High Availability

Patramanggala Cloud implements a High Availability architecture using two Nextcloud application nodes behind HAProxy.

HAProxy continuously performs health checks on both backend nodes. If one node becomes unavailable, incoming requests are automatically redirected to the remaining healthy node without requiring manual intervention.

This architecture minimizes downtime and improves service availability for village administrative operations.

## Monitoring Architecture

Infrastructure monitoring is implemented using Uptime Kuma.

The monitoring service periodically checks the availability of:

- HAProxy Reverse Proxy
- Nextcloud HTTPS Endpoint
- Nextcloud Node 1
- Nextcloud Node 2

Whenever a monitored service changes its status, Uptime Kuma automatically sends real-time notifications to administrators via Telegram Bot.

## Native Web Application Firewall

Instead of deploying ModSecurity, this project implements a lightweight Native Web Application Firewall using HAProxy Access Control Lists (ACL).
To improve security without introducing additional middleware, this project implements a lightweight Native Web Application Firewall using HAProxy Access Control Lists (ACL).
Implemented protection includes:

- HTTP Method Filtering
- Hidden File Protection
- Sensitive Directory Protection
- Scanner Detection
- Rate Limiting
- Security Headers

## Infrastructure Summary

The Patramanggala Cloud infrastructure combines High Availability, secure remote access, lightweight request filtering, and real-time monitoring into a single Docker-based platform.

By integrating HAProxy, Nextcloud, MariaDB, Redis, Tailscale, and Uptime Kuma, the system provides a secure and resilient private cloud solution for village administrative services.
