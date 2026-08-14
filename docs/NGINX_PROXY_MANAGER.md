# Service Documentation: Nginx Proxy Manager (NPM)

## Overview
* **Host IP:** `10.0.0.106`
* **Ports:** `80` (HTTP), `443` (HTTPS), `81` (Admin Web UI)
* **Primary Role:** Reverse proxy, local SSL termination, and wildcard certificate automation.

---

## Architecture & SSL Strategy
* Uses Cloudflare DNS-01 API challenges to automatically provision and renew Let's Encrypt wildcard certificates (`*.damonditrichs.com`).
* Combines public Cloudflare DNS records (pointing to local IPs as "DNS Only") with local Pi-hole split-DNS routing to allow seamless internal HTTPS access without exposing services to the public internet.