# Backup Strategy

## Overview

This document describes the backup strategy implemented for Patramanggala Cloud.

The objective is to ensure that application data, configuration files, and infrastructure settings can be restored in case of hardware failure, software corruption, or accidental deletion.

---

# Backup Scope

The following components should be included in routine backups.

| Component | Required |
|-----------|:--------:|
| MariaDB Database | ✅ |
| Nextcloud Data | ✅ |
| Docker Compose Configuration | ✅ |
| Environment Configuration (.env) | ✅ |
| HAProxy Configuration | ✅ |
| Native WAF Configuration | ✅ |
| Uptime Kuma Database | ✅ |

---

# Database Backup

MariaDB stores all Nextcloud metadata including:

- User accounts
- File metadata
- Sharing configuration
- Application settings

Create a database backup using:

```bash
docker exec patramanggala_cloud-db \
mysqldump -u root -p nextcloud > backup-nextcloud.sql
```

Store the backup file in a secure location.

---

# Nextcloud Data Backup

Nextcloud user files are stored in:

```text
/mnt/storage/nextcloud-data
```

Backup the directory using:

```bash
sudo rsync -avh \
/mnt/storage/nextcloud-data \
/backup/nextcloud-data
```

---

# Docker Configuration Backup

Backup the deployment configuration.

Recommended files:

- docker-compose.yml
- docker-compose.yml.bak
- .env

Example:

```bash
cp docker-compose.yml /backup/
cp .env /backup/
```

---

# HAProxy Configuration Backup

Backup both HAProxy configurations.

Files:

- haproxy.cfg
- haproxy-waf.cfg

Example:

```bash
cp haproxy/*.cfg /backup/
```

---

# Native WAF Backup

Backup the Native WAF configuration.

Recommended directories:

- waf/
- haproxy/

These directories contain:

- ACL Rules
- Security Configuration
- WAF Documentation

---

# Uptime Kuma Backup

Monitoring configuration is stored inside the SQLite database.

Backup:

```text
services/monitoring/uptime-kuma/kuma.db
```

Copy the database.

```bash
cp services/monitoring/uptime-kuma/kuma.db \
/backup/
```

---

# Git Repository Backup

Project documentation and infrastructure configuration are version controlled using Git.

Repository includes:

- Documentation
- Docker Compose
- HAProxy Configuration
- Native WAF Configuration
- Scripts

GitHub should be considered an additional backup for infrastructure configuration.

---

# Restore Procedure

Recovery order is recommended as follows:

1. Restore Docker configuration.
2. Restore MariaDB database.
3. Restore Nextcloud storage.
4. Restore HAProxy configuration.
5. Restore Native WAF configuration.
6. Restore Uptime Kuma database.
7. Restart Docker containers.

---

# Backup Verification

Verify that backup files exist.

Example:

```bash
ls -lh /backup
```

Verify database dump.

```bash
file backup-nextcloud.sql
```

Verify Nextcloud data.

```bash
du -sh /mnt/storage/nextcloud-data
```

---

# Backup Schedule

Recommended schedule.

| Component | Frequency |
|-----------|-----------|
| MariaDB | Daily |
| Nextcloud Data | Daily |
| Docker Configuration | Weekly |
| HAProxy Configuration | After Changes |
| Native WAF Configuration | After Changes |
| Uptime Kuma Database | Weekly |
| GitHub Repository | Every Commit |

---

# Best Practices

- Keep multiple backup copies.
- Store backups on a separate storage device.
- Test restoration periodically.
- Encrypt sensitive backups.
- Maintain backup version history.

---

# Summary

Patramanggala Cloud implements a multi-layer backup strategy covering application data, infrastructure configuration, monitoring data, and project documentation.

This approach improves disaster recovery capability while minimizing data loss and service downtime.
