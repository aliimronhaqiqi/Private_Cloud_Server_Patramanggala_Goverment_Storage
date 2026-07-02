# System Architecture

## Components

- Ubuntu Server 24.04 LTS
- Docker Compose
- HAProxy Reverse Proxy
- Native WAF (HAProxy ACL)
- Nextcloud Node 1
- Nextcloud Node 2
- MariaDB
- Redis
- Storage HDD
- Tailscale VPN
- HTTPS (Tailscale TLS Certificate)
- Uptime Kuma
- Telegram Bot
---

## Architecture Diagram

```text
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

Uptime Kuma
      │
      ├── Monitor HAProxy
      ├── Monitor HTTPS Endpoint
      ├── Monitor Nextcloud Node 1
      └── Monitor Nextcloud Node 2
             │
             ▼
     Telegram Notification
```

## Data Flow

1. Users connect to the private cloud through the Tailscale VPN.
2. Requests are secured using HTTPS.
3. HAProxy receives incoming requests and performs health checks.
4. HAProxy distributes traffic to the available Nextcloud application node using Round Robin load balancing.
5. The selected Nextcloud node processes the request.
6. Nextcloud interacts with MariaDB for metadata, Redis for caching, and Storage HDD for file storage.
7. The response is returned to the user through HAProxy.
## High Availability

Patramanggala Cloud implements a High Availability architecture using two Nextcloud application nodes behind HAProxy.

HAProxy continuously performs health checks on both backend nodes. If one node becomes unavailable, incoming requests are automatically redirected to the remaining healthy node without requiring manual intervention.

This architecture minimizes downtime and improves service availability for village administrative operations.

## Monitoring Flow

Uptime Kuma periodically checks:

- HAProxy Reverse Proxy
- HTTPS Endpoint
- Nextcloud Node 1
- Nextcloud Node 2

If a monitored service changes its status, Uptime Kuma immediately sends a notification to administrators through Telegram Bot.

## Native Web Application Firewall

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
