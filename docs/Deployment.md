# Deployment

Deployment dilakukan menggunakan Docker Compose.

## Services

- Nextcloud
- MariaDB
- Redis

Semua service berada pada Docker Bridge Network.

## Reverse Proxy

HAProxy digunakan sebagai Reverse Proxy HTTPS.

## VPN

Seluruh akses dilakukan melalui jaringan Tailscale menggunakan MagicDNS.
