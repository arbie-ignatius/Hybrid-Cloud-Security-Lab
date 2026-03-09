# Hybrid Cloud Security Lab  
## Build Log – Session 1  
### Proxmox Hypervisor Deployment

## Objective
Deploy a functioning Proxmox Virtual Environment (PVE) hypervisor to serve as the primary compute node for a cybersecurity and hybrid cloud homelab.

---

# Hardware Platform

Host Node  
HP Laptop

Resources
- CPU: 4 Cores
- RAM: 32 GB
- Storage: ~1 TB NVMe

Supporting Infrastructure
- Managed Ethernet Switch
- Unmanaged Ethernet Switch
- Ethernet Patch Panel
- Surface Pro (management workstation)

---

# Hypervisor Deployment

Hypervisor Software  
Proxmox Virtual Environment 9.1

Node Name

atlas-pve01

Management Interface

https://192.168.88.50:8006

---

# Issues Encountered

## Issue 1 – Proxmox Web Interface Unreachable

### Symptom
Management interface could not be reached via browser.

Ping results returned:

Destination host unreachable

### Root Cause
Physical network path through patch panel and switches was misconfigured.

### Resolution
Validated and corrected network path:

Managed Switch → Patch Panel → Unmanaged Switch → Proxmox Host

Link lights confirmed successful Layer 1 connectivity.

---

## Issue 2 – Authentication Failure

### Symptom
Web interface login returned:

authentication failure (401)

### Root Cause
Incorrect or forgotten root password during initial login.

### Resolution
Password reset performed through local console.

Command used:

passwd

Password successfully updated and web login restored.

---

## Issue 3 – Package Update Error

### Symptom
Proxmox task log displayed:

Update package database failed

### Root Cause
Default repository configured for Proxmox Enterprise subscription.

### Resolution
Configured the community repository.

File modified:

/etc/apt/sources.list.d/pve-enterprise.list

Repository added:

deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription

System updated using:

apt update  
apt full-upgrade -y

---

# Current Lab Status

Hypervisor successfully deployed and operational.

Node

atlas-pve01

Management Access

https://192.168.88.50:8006

Available Resources
- CPU: 4 cores
- RAM: ~32 GB
- Storage: ~1 TB NVMe

---

# Planned Virtual Machines

Kali Linux  
Offensive security testing platform.

Ubuntu Server  
Log aggregation and security monitoring platform.

Windows Server  
Active Directory and enterprise lab environment.

pfSense  
Virtual firewall and network segmentation platform.

---

# Next Steps

1. Validate Proxmox network bridge configuration.
2. Upload operating system ISO images.
3. Deploy initial virtual machines.
4. Configure segmented virtual networks.
5. Implement logging and monitoring stack.

---

# Notes

This node serves as the primary hypervisor for the Hybrid Cloud Security Lab.  
Future nodes may be added to expand the cluster and simulate multi-node infrastructure environments.