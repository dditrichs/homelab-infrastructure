# Service Documentation: Jellyfin Media Server (LXC 102)

## Container Overview
* **CT ID:** `102`
* **Hostname:** `jellyfin`
* **Local IP Address:** `10.0.0.102`
* **Tailscale IP:** `Tailscale Mesh IP`
* **Port:** `8096` (HTTP Web UI)
* **OS:** Debian 13 (Trixie)
* **Root Storage:** `local-lvm` (NVMe/SSD for OS & Database performance)
* **Media Storage:** `seagate-pool` (4TB HDD ZFS Pool via Proxmox Bind Mount)
* **Deployment Method:** Docker Compose 

---

## Architecture & Storage Configuration

### OS & Application Separation
To optimize system performance and storage efficiency, the deployment isolates the operating system from heavy media storage:
1. **Application Runtime & Database (`local-lvm`):** Hosted on high-speed SSD storage to ensure snappy database queries, fast metadata retrieval, and quick web UI rendering.
2. **Bulk Media Assets (`seagate-pool`):** Attached via a Proxmox LXC bind mount to map the local 4TB ZFS hard drive array directly into the container filesystem.

---

## Network & Access Strategy

To avoid the performance bottlenecks and metadata/image-loading issues often introduced by routing high-bandwidth streaming through internal reverse proxy layers, Jellyfin is configured with split direct access paths:

* **Local Access:** Accessed directly via local IP and port (`10.0.0.102:8096`) for unthrottled local playback, full metadata asset loading, and local device casting.
* **Tailscale Access:** Accessed directly via the private Tailscale mesh network IP (`8096`), ensuring secure, encrypted remote streaming without proxy overhead.

---

## Maintenance & Service Verification

### Checking Service Status
To verify the Jellyfin server status directly on the container:
```bash
systemctl status jellyfin