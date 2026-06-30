# System Architecture

## Components

- Ubuntu Server 24.04 LTS
- Docker Compose
- Nextcloud
- MariaDB
- Redis
- HAProxy
- Tailscale VPN
- HTTPS Certificate

---

## Architecture Diagram

```
Staff Device
      │
Tailscale VPN
      │
MagicDNS HTTPS
      │
HAProxy
      │
Nextcloud
 ├────────────┐
 │            │
Redis      MariaDB
 │
Storage HDD
```

---

## Data Flow

User → Tailscale → HTTPS → HAProxy → Nextcloud → MariaDB / Redis → Storage
