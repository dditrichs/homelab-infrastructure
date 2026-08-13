# Proxmox VE Homelab Infrastructure

[![Proxmox VE](https://img.shields.io/badge/Proxmox_VE-8.x-E57008?style=flat&logo=proxmox)](https://www.proxmox.com)
[![Debian](https://img.shields.io/badge/Debian-12-A81D33?style=flat&logo=debian)](https://www.debian.org)
[![Pi-hole](https://img.shields.io/badge/Pi--hole-v6-96060C?style=flat&logo=pi-hole)](https://pi-hole.net)
[![Unbound](https://img.shields.io/badge/Unbound-DNSSEC-4183C4)](https://nlnetlabs.nl/projects/unbound/about/)
[![Uptime Kuma](https://img.shields.io/badge/Uptime_Kuma-Monitoring-5CDB95?style=flat&logo=uptime-kuma)](https://github.com/louislam/uptime-kuma)
[![Open WebUI](https://img.shields.io/badge/Open_WebUI-v0.5-008080?style=flat&logo=open-webui&logoColor=white)](https://github.com/open-webui/open-webui)
[![Ollama](https://img.shields.io/badge/Ollama-Local_AI-000000?style=flat&logo=ollama&logoColor=white)](https://ollama.com)

A hands-on, evolving homelab project documenting core network services, Proxmox virtualization, and systems administration.

---

## Repository Structure

* `configs/` — Sanitized configuration files for homelab services.
* `configs/unbound/` — Recursive DNS resolver configuration (`pi-hole.conf`).
* `docs/` — Technical documentation and verification testing logs.
* `docs/UPTIME_KUMA.md` — Uptime Kuma installation and monitor configurations.
* `docs/OPEN_WEBUI.md` — Open WebUI & Ollama LXC container setup, GPU passthrough, and active models.

---

## Active Infrastructure Services 

| Service | Host / Container | IP / Port | Function |
| :--- | :--- | :--- | :--- |
| **Proxmox VE** | Bare-Metal Host | `10.0.0.147` | Primary Hypervisor Platform |
| **Pi-hole v6** | LXC 100 (Debian) | `10.0.0.100:53` | Network-wide Ad & Tracker Filtering |
| **Unbound** | LXC 100 (Debian) | `127.0.0.1:5335` | Local Recursive DNSSEC Resolver |
| **Uptime Kuma** | LXC 101 (Debian) | `10.0.0.101:3001` | Infrastructure & Service Health Monitoring |
| **Open WebUI / Ollama** | LXC 104 (Debian) | `10.0.0.104:3000` | Self-Hosted Local AI LLM Service (GTX 1650 SUPER Passthrough) |

---

## DNS Validation Commands

```bash
# 1. Invalid signature (Must return SERVFAIL)
dig fail01.dnssec.works @127.0.0.1 -p 5335

# 2. Valid signature (Must return NOERROR with 'ad' flag)
dig cloudflare.com @127.0.0.1 -p 5335
