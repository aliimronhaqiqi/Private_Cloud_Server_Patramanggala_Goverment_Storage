# Installation Guide

## System Requirements

- Ubuntu Server 24.04 LTS
- Docker Engine
- Docker Compose
- Git
- Tailscale
- Internet Connection

---

## Install Docker

```bash
sudo apt update
sudo apt install docker.io docker-compose-v2 -y
```

---

## Clone Repository

```bash
git clone git@github.com:aliimronhaqiqi/Patramanggala_Cloud.git
cd Patramanggala_Cloud
```

---

## Configure Environment

Edit file `.env` sesuai kebutuhan.

---

## Run Docker

```bash
docker compose up -d
```

---

## Verify

```bash
docker ps
```

Semua container harus berstatus **Up**.
