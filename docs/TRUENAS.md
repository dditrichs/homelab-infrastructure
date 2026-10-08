# TrueNAS Storage & Backup VM

## Overview
Virtual Machine (VM 107) running TrueNAS to provide network-attached storage (NAS) and host daily automated Windows File History backups from the primary workstation.

## Specifications
* **VM ID:** 107
* **OS:** TrueNAS
* **RAM:** 8 GB
* **vCPUs:** 2 Cores (1 Socket, x86-64-v2-AES)
* **Storage:** 
  * OS Drive: 32 GB (`local-lvm:vm-107-disk-0`)
  * Data Pool: Dedicated HDD passthrough via disk-by-id
* **Network:** VirtIO on `vmbr0`

## Configuration & Services
* **SMB Share:** Configured on the storage pool for local network access.
* **Backup Workflow:** Serves as the designated network destination target for scheduled daily Windows File History backups.