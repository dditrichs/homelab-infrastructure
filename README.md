# Proxmox VE Homelab Infrastructure

[![Proxmox VE](https://img.shields.io/badge/Proxmox_VE-9.x-E57008?style=flat&logo=proxmox)](https://www.proxmox.com)
[![Debian](https://img.shields.io/badge/Debian-12-A81D33?style=flat&logo=debian)](https://www.debian.org)
[![Pi-hole](https://img.shields.io/badge/Pi--hole-v6-96060C?style=flat&logo=pi-hole)](https://pi-hole.net)
[![Unbound](https://img.shields.io/badge/Unbound-DNSSEC-4183C4)](https://nlnetlabs.nl/projects/unbound/about/)
[![Uptime Kuma](https://img.shields.io/badge/Uptime_Kuma-Monitoring-5CDB95?style=flat&logo=uptime-kuma)](https://github.com/louislam/uptime-kuma)
[![Minecraft](https://img.shields.io/badge/Minecraft-Java_Server-2E7D32?style=flat&logo=minecraft&logoColor=white)](https://www.minecraft.net)
[![Jellyfin](https://img.shields.io/badge/Jellyfin-Media_Server-00A4DC?style=flat&logo=jellyfin&logoColor=white)](https://jellyfin.org)
[![Open WebUI](https://img.shields.io/badge/Open_WebUI-v0.5-008080?style=flat&logo=open-webui&logoColor=white)](https://github.com/open-webui/open-webui)
[![Ollama](https://img.shields.io/badge/Ollama-Local_AI-000000?style=flat&logo=ollama&logoColor=white)](https://ollama.com)
[![Nginx Proxy Manager](https://img.shields.io/badge/Nginx_Proxy_Manager-SSL_Proxy-009900?style=flat&logo=nginxproxymanager&logoColor=white)](https://nginxproxymanager.com)
[![Vaultwarden](https://img.shields.io/badge/Vaultwarden-Password_Manager-175DDC?style=flat&logo=bitwarden&logoColor=white)](https://github.com/dani-garcia/vaultwarden)
[![Tailscale](https://img.shields.io/badge/Tailscale-Mesh_VPN-2A3748?style=flat&logo=tailscale&logoColor=white)](https://tailscale.com)

A hands-on, evolving homelab project documenting core network services, Proxmox virtualization, and systems administration.

---

## Repository Structure

* `configs/` — Sanitized configuration files for homelab services.
* `configs/docker/` — Docker Compose deployment files for containerized services.
* `configs/lxc/` — Proxmox VE container definition files (hardware, bind mounts, GPU passthrough).
* `configs/unbound/` — Recursive DNS resolver configuration (`pi-hole.conf`).
* `docs/` — Technical documentation and verification testing logs.
* `docs/UPTIME_KUMA.md` — Uptime Kuma installation and monitor configurations.
* `docs/JELLYFIN.md` — Jellyfin media server deployment, ZFS storage bind mounts, and dual local/Tailscale setup.
* `docs/MINECRAFT.md` — Dedicated Minecraft server VM specs, network configuration, and Docker Compose setup.
* `docs/OPEN_WEBUI.md` — Open WebUI & Ollama LXC container setup, GPU passthrough, and active models.
* `docs/VAULTWARDEN.md` — Vaultwarden password manager setup and SSL documentation.
* `docs/NGINX_PROXY_MANAGER.md` — Nginx Proxy Manager architecture and wildcard SSL guide.
* `docs/TAILSCALE.md` — Tailscale mesh network and secure remote access routing.

---

## Active Infrastructure Services 

| Service | Host / Container | IP / Port | Function |
| :--- | :--- | :--- | :--- |
| **Proxmox VE** | Bare-Metal Host | `10.0.0.147` | Primary Hypervisor Platform |
| **Pi-hole v6** | LXC 100 (Debian) | `10.0.0.100:53` | Network-wide Ad & Tracker Filtering |
| **Unbound** | LXC 100 (Debian) | `127.0.0.1:5335` | Local Recursive DNSSEC Resolver |
| **Uptime Kuma** | LXC 101 (Debian) | `10.0.0.101:3001` | Infrastructure & Service Health Monitoring |
| **Jellyfin (Local)** | LXC 102 (Debian) | `10.0.0.102:8096` | High-bandwidth local streaming, ZFS storage bind mounts, & asset loading |
| **Jellyfin (Tailscale)** | LXC 102 / Tailnet | Tailscale IP: `8096` | Secure encrypted remote streaming over tailnet |
| **Minecraft Server** | VM 103 (Ubuntu) | `10.0.0.103:25565` | Dedicated Minecraft Server (Docker Compose) |
| **Open WebUI / Ollama** | LXC 104 (Debian) | `10.0.0.104:3000` | Self-Hosted Local AI LLM Service (GTX 1650 SUPER Passthrough) |
| **Vaultwarden** | Docker Container | `10.0.0.105:8080` | Self-Hosted Password Manager (Secured via NPM & SSL) |
| **Nginx Proxy Manager** | Bare-Metal / Docker | `10.0.0.106:81` | Reverse Proxy & Wildcard SSL Certificate Management |

---

## Jellyfin Network & Access Strategy

To avoid the performance bottlenecks and metadata/image-loading issues often introduced by routing high-bandwidth streaming through internal reverse proxy layers, Jellyfin is configured with split access paths:

* **`jellyfin-local`:** Accessed directly via local IP and port (`10.0.0.102:8096`) for unthrottled local playback, full metadata asset loading, and local device casting.
* **`jellyfin-tailscale`:** Accessed directly via the private Tailscale mesh network IP, ensuring encrypted remote connectivity without proxy overhead.

---

## DNS Validation Commands

```bash
# 1. Invalid signature (Must return SERVFAIL)
dig fail01.dnssec.works @127.0.0.1 -p 5335

# 2. Valid signature (Must return NOERROR with 'ad' flag)
dig cloudflare.com @127.0.0.1 -p 5335