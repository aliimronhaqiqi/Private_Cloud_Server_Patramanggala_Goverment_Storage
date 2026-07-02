# Troubleshooting Guide

## Overview

This document summarizes common issues encountered during the deployment, operation, and maintenance of Patramanggala Cloud.

Each troubleshooting case is based on the actual implementation and testing experience throughout the development of this project.

---

# HAProxy Backend Down

## Problem

One or more backend servers appear as **DOWN** on the HAProxy Statistics page.

## Possible Causes

- Nextcloud container stopped
- Incorrect backend port
- Failed health check
- Docker network issue

## Diagnosis

```bash
docker ps

docker logs patramanggala_cloud-app

curl http://localhost:8080/status.php

curl http://localhost:8082/status.php
```

## Solution

- Start the stopped container.
- Verify backend ports.
- Confirm `/status.php` returns a valid JSON response.
- Reload HAProxy configuration if necessary.

---

# High Availability Failover

## Problem

One Nextcloud node becomes unavailable.

## Expected Behaviour

HAProxy automatically removes the unhealthy backend and forwards requests to the healthy node.

## Verification

```bash
docker stop patramanggala_cloud-app
```

Refresh the Nextcloud web interface.

If the application remains accessible, the failover mechanism is working correctly.

Restore the node:

```bash
docker start patramanggala_cloud-app
```

---

# Uptime Kuma Connection Refused

## Problem

Browser displays:

```
ERR_CONNECTION_REFUSED
```

when accessing:

```
http://SERVER-IP:3001
```

## Possible Causes

- Uptime Kuma container stopped
- SQLite database missing
- Port 3001 unavailable

## Diagnosis

```bash
docker ps -a

docker logs patramanggala_uptime_kuma

sudo ss -tulpn | grep 3001

curl http://localhost:3001
```

## Solution

Restore:

```
services/monitoring/uptime-kuma/kuma.db
```

Restart the container.

```bash
docker start patramanggala_uptime_kuma
```

---

# Telegram Notification Failed

## Problem

Telegram notification test returns:

```
401 Unauthorized
```

## Possible Causes

- Invalid Bot Token
- Incorrect Chat ID
- Bot has not been started

## Solution

- Create a new Bot Token using BotFather.
- Start the Telegram bot.
- Verify the Chat ID.
- Update the Telegram notification configuration inside Uptime Kuma.

---

# HTTPS Cannot Be Accessed

## Problem

HTTPS endpoint cannot be reached.

## Diagnosis

```bash
tailscale status

sudo ss -tulpn | grep 443
```

Verify:

- Tailscale is connected.
- HAProxy is listening on port 443.
- TLS certificate is available.

## Solution

Restart HAProxy if required and verify the Tailscale TLS certificate.

---

# MagicDNS Cannot Be Accessed

## Problem

MagicDNS hostname is unreachable.

## Possible Causes

- MagicDNS disabled
- Device not connected to Tailscale
- DNS propagation delay

## Solution

Verify:

```bash
tailscale status
```

Use the Tailscale IP address temporarily until MagicDNS becomes available.

---

# Trusted Domain Error

## Problem

Nextcloud displays:

```
Access through untrusted domain
```

## Solution

Edit:

```
config/config.php
```

Add the required hostname or IP address to the trusted domains list.

---

# Git Push Rejected

## Problem

```
! [rejected] (fetch first)
```

## Cause

The remote repository contains commits that are not available locally.

## Solution

```bash
git pull origin feature/waf

git push origin feature/waf
```

---

# Nested Git Repository

## Problem

A Git repository is accidentally cloned inside another Git repository.

Example:

```
Patramanggala_Cloud/

└── Patramanggala_Cloud/
```

## Cause

Running:

```bash
git clone
```

inside an existing repository.

## Solution

Keep the primary repository and remove the duplicated clone directory.

---

# Runtime Database Missing

## Problem

Uptime Kuma fails to start after the runtime database is moved.

## Cause

The SQLite database (`kuma.db`) was removed from the Docker bind mount directory.

## Solution

Restore:

```
services/monitoring/uptime-kuma/kuma.db
```

Restart the container.

Never commit runtime databases to Git.

Ignore them using:

```
.gitignore
```

---

# Docker Permission Denied

## Problem

Permission denied when accessing mounted files.

## Diagnosis

```bash
ls -lah
```

Check the file owner.

## Solution

```bash
sudo chown -R username:username directory
```

Replace `username` with the correct Linux account.

---

# Native WAF Blocking Requests

## Problem

The client receives:

```
403 Forbidden
```

## Possible Causes

- TRACE request
- CONNECT request
- Scanner User-Agent
- Hidden file access
- Sensitive directory request

## Solution

Review the HAProxy ACL rules and verify whether the request should be allowed.

---

# Common Diagnostic Commands

```bash
docker ps

docker ps -a

docker compose ps

docker compose logs

docker logs <container>

tailscale status

curl http://localhost:8080/status.php

curl http://localhost:8082/status.php

sudo ss -tulpn

git status

git log --oneline
```

---

# Best Practices

- Check container status before restarting services.
- Read service logs before applying changes.
- Keep runtime databases outside Git version control.
- Test failover after infrastructure changes.
- Verify Telegram notifications after monitoring updates.
- Maintain backup copies before modifying production configurations.

---

# Summary

The troubleshooting procedures documented here are based on real deployment experience during the implementation of Patramanggala Cloud.

Following these diagnostic and recovery steps helps reduce downtime, improve system reliability, and simplify infrastructure maintenance.
