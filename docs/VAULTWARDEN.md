# Service Documentation: Vaultwarden Password Manager

## Overview
* **Service:** Vaultwarden (Unofficial Bitwarden compatible server written in Rust)
* **IP / Port:** `10.0.0.105:80` (Proxied via NPM)
* **Subdomain:** `vault.damonditrichs.com`
* **Deployment Method:** Docker Compose

---

## Security & SSL Configuration
* **Encryption:** Secured with a valid Let's Encrypt wildcard SSL certificate (`*.damonditrichs.com`) managed through Nginx Proxy Manager via **Cloudflare DNS authentication**.
* **Websockets:** Enabled to support real-time vault sync across client devices.