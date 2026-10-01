# OPNsense Perimeter Defense & Resilient DNS Architecture

<a href="https://github.com/gregorymoorejr">← Back to Main Portfolio</a>

## Overview
This project details the design, implementation, and hardening of my home network's perimeter defense and core routing architecture. Built on an **OPNsense** firewall, the environment enforces strict least-privilege access using multi-VLAN segmentation combined with a robust, multi-layered DNS resolution and filtering stack.

---

## Architecture & Traffic Flow

[ Internet ]
│
▼
[ OPNsense Firewall ] (VLAN 90 - Infrastructure)
│
├──> [ Management Subnet (VLAN 100) ] ──> [ SysLinuxOS / Surface Pro 3 Console ]
├──> [ Monitoring Stack (VLAN 110) ] ───> [ Zabbix / Dell Inspiron 5566 ]
├──> [ SOC / SIEM (VLAN 120) ] ─────────> [ Wazuh / Dell Precision 5530 ]
├──> [ Storage (VLAN 130) ] ────────────> [ OpenMediaVault / Dell Inspiron 5568 ]
├──> [ App Servers (VLAN 80) ] ──────────> [ Proxmox VE / Dell Precision 7530 ]
├──> [ Trusted / Client (VLAN 150) ]
├──> [ Home Office / Guest (VLAN 160) ]
├──> [ Entertainment (VLAN 140) ]
└──> [ IoT Devices (VLAN 170) ]

### Core Hardware & Infrastructure Layer (VLAN 90)
* **Firewall & Routing:** OPNsense core routing engine.
* **Network Backbone:** Netgear Orbi Pro WiFi mesh system, MoCA adapters, and a Grandstream GWN7721 managed switch.

---

## VLAN & Subnet Breakdown

| VLAN ID | Subnet Zone | Purpose & Dedicated Hardware Implementation |
| :--- | :--- | :--- |
| **VLAN 80** | Application Servers | Hosts application containers/servers running on Proxmox VE hosted on a repurposed **Dell Precision 7530**. |
| **VLAN 90** | Infrastructure | Core network backbone for OPNsense, Netgear Orbi Pro WiFi mesh, MoCA adapters, and the Grandstream GWN7721 managed switch. |
| **VLAN 100** | Management Subnet | Dedicated console management network running **SysLinuxOS on a Microsoft Surface Pro 3**. Central administrative point for all infrastructure devices and servers. |
| **VLAN 110** | Network Monitoring | Dedicated subnet for infrastructure health monitoring via **Zabbix** running on a repurposed **Dell Inspiron 15 5566**. |
| **VLAN 120** | SOC / SIEM | Dedicated subnet for security operations and log analysis via **Wazuh SIEM** running on a repurposed **Dell Precision 5530**. |
| **VLAN 130** | Network Attached Storage | Dedicated subnet for data storage utilizing **OpenMediaVault** running on a repurposed **Dell Inspiron 15 5568**. |
| **VLAN 140** | Home Entertainment | Subnet for smart TVs, gaming consoles, and network-enabled desktop media players. |
| **VLAN 150** | Main / Trusted | Primary subnet for personal computers, smartphones, and network printers. |
| **VLAN 160** | Home Office & Guest | Segmented network allocated for home office productivity and guest wireless access. |
| **VLAN 170** | IoT Subnet | Isolated zone for smart home appliances, thermostats, and security cameras. |

---

## DNS Security & Resolution Pipeline
* **AdGuard Home:** Acts as the primary network-wide DNS sinkhole, intercepting telemetry, trackers, and malicious domains.
* **Unbound DNS:** Configured as the upstream recursive resolver for AdGuard Home, performing direct DNS queries to authoritative root servers.
* **Dnsmasq:** Handles local DHCP-driven name resolution and internal network routing for local container and host names.

---

## Future Roadmap & Enhancements
* **Zenarmor Integration:** Deployment of Layer 7 deep packet inspection (DPI) and application-layer telemetry on OPNsense.
* **CrowdSec Integration:** Implementation of collaborative security agents and firewall bouncers for active threat intelligence.
* **Q-Feeds Integration:** Incorporation of custom threat intelligence feeds to tighten perimeter block policies.

<a href="https://github.com/gregorymoorejr">← Back to Main Portfolio</a>
