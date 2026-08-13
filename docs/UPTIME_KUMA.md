# Service Documentation: Uptime Kuma (LXC 101)

## Container Overview
* **CT ID:** `101`
* **Hostname:** `kuma`
* **IP Address:** `10.0.0.101`
* **Port:** `3001` (Web Dashboard)
* **Storage:** `local-lvm` (SSD)
* **Specs:** 2 vCPU / 2048 MB RAM

---

## Configured Monitors

### 1. Pi-hole Service Stack (`10.0.0.100`)

| Monitor Name | Type | Target | Port | Interval | Purpose / Failure Mode |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Pi-hole Ping** | Ping | `10.0.0.100` | — | 60s | Host/Container Liveness (Checks if LXC 100 is online) |
| **Pi-hole DNS** | DNS | `google.com` | `53` (Resolver: `10.0.0.100`) | 60s | Resolution Health (Checks if `pihole-FTL` is serving queries) |
| **Pi-hole Admin Web** | HTTP(s) | `http://10.0.0.100/admin` | `80` | 60s | Web UI Availability (Checks web server/lighttpd status) |

---

## Troubleshooting Quick Reference

* **Ping Down:** LXC container 100 is stopped or unroutable. Check Proxmox VE host (`10.0.0.147`).
* **Ping UP / DNS Down:** Container running, but FTL engine crashed. SSH into `10.0.0.100` and run `systemctl status pihole-FTL`.
* **DNS UP / HTTP Down:** DNS works, but administrative interface is unresponsive.