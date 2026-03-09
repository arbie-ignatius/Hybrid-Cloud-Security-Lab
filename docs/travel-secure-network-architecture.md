# Portable Secure Travel Network Setup

**Author:** Arbie Ignatius Melendrez  
**Purpose:** Secure, segmented networking architecture for hotel and travel environments

---

## 1. Overview

This document outlines a portable edge networking setup designed to:

- Isolate personal and work devices from public hotel networks
- Provide centralized network control
- Enforce firewall and traffic policies
- Maintain operational flexibility while traveling

This configuration has been deployed in hotel environments to create a controlled internal network over untrusted infrastructure.

---

## 2. Hardware Stack

### Primary Devices

- **GL.iNet Puli (GL-X750 Series)** – Travel router (primary gateway)
- **Cisco Router (SIPR support)** – Dedicated routing device for SIPR connectivity
- **GL.iNet Mudi** – LTE-capable travel router (optional failover)
- **FileHub RP-WD009** – Auxiliary travel router and storage bridge
- **Compact unmanaged “dummy” switch** – Inline Ethernet distribution

---

## 3. Network Architecture (Hotel Deployment)

### Physical Flow

Hotel Wall Ethernet  
↓  
Unmanaged Dummy Switch  
↓  
Branch 1 → GL.iNet Puli (WAN Port)  
↓  
Internal Secure Network (Wi-Fi + LAN for personal + work devices)

Branch 2 → Cisco Router  
↓  
SIPR Workstation (per policy requirements)

---

## 4. Security Design

### 4.1 Network Segmentation

The unmanaged switch distributes ISP connectivity to two logically separate routing paths:

**Path A:**  
GL.iNet Puli → Personal and commercial work devices

**Path B:**  
Cisco Router → SIPR workstation

Segmentation is enforced at the routing level, not the switching layer.

The Puli acts as a boundary device between untrusted hotel infrastructure and trusted internal devices.

The Cisco router maintains a separate routing domain for SIPR connectivity to preserve compliance and isolation requirements.

---

### 4.2 Firewall Configuration

Custom firewall rules are applied on the Puli to:

- Restrict unnecessary inbound traffic
- Control outbound traffic as required
- Limit exposure to hotel LAN broadcast traffic
- Prevent lateral movement between internal devices (where configured)

The Cisco router configuration for SIPR is maintained separately in accordance with mission and policy requirements.

---

### 4.3 Captive Portal Handling

The Puli authenticates once to the hotel captive portal, allowing internal non-SIPR devices to route through a single authenticated session.

SIPR connectivity via the Cisco router follows established operational procedures and authentication requirements.

---

### 4.4 VPN Usage

- Work VPN clients operate from internal devices connected to the Puli.
- SIPR traffic routes exclusively through the Cisco router.
- The travel router may optionally run VPN services depending on mission requirements.

---

## 5. Performance Considerations

Observed performance limitations in hotel environments may be caused by:

- Hotel bandwidth restrictions
- Double Network Address Translation (NAT)
- Encryption overhead from VPNs
- Firewall inspection processing
- 2.4 GHz Wi-Fi congestion

### Mitigation Steps

- Prefer 5 GHz wireless when available
- Test direct Ethernet to isolate Wi-Fi bottlenecks
- Adjust Maximum Transmission Unit (MTU) settings if required
- Disable unnecessary inspection features during high-bandwidth tasks

---

## 6. Operational Benefits

- Controlled ingress and egress traffic
- Reduced exposure to public network threats
- Centralized management of travel devices
- Logical separation of SIPR and non-SIPR traffic
- Portable edge networking capability
- Repeatable deployment process

---

## 7. Optional Enhancements (Future Integration)

- Site-to-site VPN tunnel back to home lab
- LTE failover using GL.iNet Mudi
- VLAN segmentation between device categories
- Intrusion detection monitoring
- Automated configuration backup scripts

---

## 8. Strategic Relevance

This portable setup demonstrates practical application of:

- Edge network security
- Network segmentation principles
- Firewall rule design
- Secure remote connectivity
- Field-deployable infrastructure architecture
- Multi-router traffic isolation for compliance-driven environments

It represents a practical implementation of secure networking practices in untrusted environments.

---

## 9. Deployment Checklist

### Before Travel

- Update firmware
- Backup router configurations
- Verify firewall rules
- Test VPN connectivity
- Validate Cisco SIPR configuration

### On Site

- Connect WAN to hotel Ethernet
- Verify dummy switch distribution
- Authenticate captive portal
- Verify firewall status
- Confirm device isolation
- Validate VPN connectivity
- Confirm SIPR routing via Cisco device

### Post-Travel

- Review logs (if enabled)
- Backup configuration changes
- Document performance observations

---

## Conclusion

This portable secure travel configuration transforms public infrastructure into a controlled, segmented network environment.

It balances mobility, operational security, compliance-driven separation requirements, and practical deployment constraints.