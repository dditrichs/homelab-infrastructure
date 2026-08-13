# Service Documentation: Dedicated Minecraft Server (VM 103)

## Virtual Machine Overview
* **VM ID:** `103`
* **Hostname:** `minecraft`
* **IP Address:** `10.0.0.103`
* **OS:** Ubuntu 22.04.5 LTS
* **Hypervisor Allocation:** 4 Cores / 8192 MB RAM / 32 GB SSD Storage (`local-lvm`)
* **Storage Controller:** `virtio-scsi-single` with `iothread=1` (Optimized I/O)
* **Deployment Method:** Docker Compose (`itzg/minecraft-server`)

---

## Network & Port Configuration

| Port | Protocol | Service / Function |
| :--- | :--- | :--- |
| `25565` | TCP / UDP | Primary Game Client Connection |

---

## Service Management

### Managing the Container
Navigate to the server directory inside VM 103 (`/home/dditrichs/minecraft`) to manage the Docker lifecycle:

```bash
# Start the server in the background
docker compose up -d

# View real-time server logs
docker compose logs -f

# Stop the server cleanly
docker compose down