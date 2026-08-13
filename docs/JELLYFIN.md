# Service Documentation: Jellyfin Media Server (LXC 102)

## Container Overview
* **CT ID:** `102`
* **Hostname:** `jellyfin`
* **IP Address:** `10.0.0.102`
* **Port:** `8096` (HTTP Web UI)
* **OS:** Debian 13 (Trixie)
* **Root Storage:** `local-lvm` (NVMe/SSD for OS & Database performance)
* **Media Storage:** `seagate-pool` (4TB HDD ZFS Pool via Proxmox Bind Mount)
* **Deployment Method:** Native Debian Systemd Service (`jellyfin.service`)

---

## Architecture & Storage Configuration

### OS & Application Separation
To optimize system performance and storage efficiency, the deployment isolates the operating system from heavy media storage:
1. **Application Runtime & Database (`local-lvm`):** Hosted on high-speed SSD storage to ensure snappy database queries, fast metadata retrieval, and quick web UI rendering.
2. **Bulk Media Assets (`seagate-pool`):** Attached via a Proxmox LXC bind mount to map the local 4TB ZFS hard drive array directly into the container filesystem.

---

## Maintenance & Service Verification

### Checking Service Status
To verify the Jellyfin server status directly on the container:
```bash
systemctl status jellyfin
```