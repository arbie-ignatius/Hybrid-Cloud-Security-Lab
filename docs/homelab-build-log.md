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

# Homelab Build Log — Observability Stack

## Date

March 9, 2026

## Environment

Proxmox VE Node: atlas-pve01
VM: lab-control (Ubuntu Server)
Container Platform: Docker + Portainer

---

# Objective

Deploy a foundational monitoring and observability stack for the homelab environment using open-source tooling.

Primary goals:

* Infrastructure health monitoring
* Container monitoring
* Network service availability checks
* Dashboard visualization
* Future alerting capability

---

# Components Deployed

### Portainer

Purpose: Docker management interface

Container:

```
portainer/portainer-ce
```

Status:
Operational

Notes:
Used as the central container orchestration interface for the lab.

---

### Prometheus

Purpose: Metrics collection and time-series database

Container:

```
prom/prometheus
```

Port:

```
9090
```

Function:
Scrapes metrics from exporters and stores them for analysis and visualization.

---

### Node Exporter

Purpose: Host system metrics exporter

Container:

```
prom/node-exporter
```

Port:

```
9100
```

Metrics exposed:

* CPU utilization
* Memory usage
* Disk IO
* Network traffic
* System load
* Filesystem usage

Metrics endpoint verified:

```
http://192.168.88.251:9100/metrics
```

---

### Grafana

Purpose: Visualization and dashboarding

Container:

```
grafana/grafana
```

Port:

```
3000
```

Dashboard installed:

```
Node Exporter Full
Dashboard ID: 1860
```

---

### Uptime Kuma

Purpose: Service uptime monitoring

Container:

```
louislam/uptime-kuma
```

Function:
Tracks availability of services and network endpoints.

---

# Network Layout

```
Node Exporter → Prometheus → Grafana
                     ↓
                Uptime Kuma
```

Prometheus collects metrics.

Grafana visualizes them.

Uptime Kuma monitors service availability.

---

# Issues Encountered

## 1. Prometheus configuration editing

Initial attempt to edit Prometheus configuration inside the container failed.

Reason:
Minimal container image lacked editing utilities such as `vi`.

Resolution:
Moved configuration management to host-based configuration files.

---

## 2. Node Exporter metrics not appearing in Grafana

Symptoms:

* Grafana dashboards showed "N/A"
* Prometheus `/targets` page only displayed `prometheus`

Root cause:
Prometheus configuration was not successfully updated inside the container.

Resolution steps:

* Created host configuration directory
* Implemented bind mount for Prometheus configuration
* Redeployed container via Portainer

---

## 3. Container networking verification

Metrics endpoint confirmed reachable via:

```
http://192.168.88.251:9100/metrics
```

Confirmed Node Exporter service is operational.

---

# Lessons Learned

### 1. Avoid editing container configurations internally

Containers are ephemeral.

Best practice:

```
Host configuration files + bind mounts
```

This ensures configuration persistence across container recreation.

---

### 2. Verify monitoring pipeline step-by-step

Correct troubleshooting order:

1. Exporter metrics endpoint
2. Prometheus scrape targets
3. Prometheus query results
4. Grafana dashboards

Skipping steps complicates troubleshooting.

---

### 3. Documentation is part of infrastructure

Maintaining a build log provides:

* repeatability
* troubleshooting reference
* portfolio evidence of engineering methodology

---

# Current Status

| Component     | Status  |
| ------------- | ------- |
| Portainer     | Running |
| Prometheus    | Running |
| Node Exporter | Running |
| Grafana       | Running |
| Uptime Kuma   | Running |

Observability stack deployed successfully.

---

# Next Phase Goals

Future enhancements planned:

### Monitoring Expansion

* Docker container monitoring
* Proxmox metrics integration
* Network device monitoring

### Alerting

* Prometheus Alertmanager
* Discord notifications
* Mobile alerts

### Security Monitoring

* Log aggregation
* anomaly detection
* security dashboards

---

# Result

A functional observability stack has been deployed and integrated into the homelab environment.

This architecture mirrors monitoring pipelines used in production environments and forms the foundation for future security, reliability, and infrastructure experimentation.


---

# Notes

This node serves as the primary hypervisor for the Hybrid Cloud Security Lab.  
Future nodes may be added to expand the cluster and simulate multi-node infrastructure environments.
