# Enterprise NOC Simulation: Troubleshooting and Defense 🌐

**Author:** Salmata Lamin
**Environment:** Cisco Packet Tracer
**Objective:** Simulate, manage, and troubleshoot an enterprise NOC network with secure VLAN segmentation and inter-VLAN routing.

---

## 🛡️ Executive Summary

This project documents the successful setup and management of a simulated enterprise network segment. It showcases competency in **VLAN segmentation**, **Inter-VLAN routing (Router-on-a-Stick)**, and **proactive incident response**. The report details the diagnosis and resolution of a connectivity loss incident and the implementation of a separate Management VLAN for security.

### Key Skills Demonstrated
* **VLAN Implementation:** Segmenting the network into Admin (VLAN 10), Operations (VLAN 20), and Security (VLAN 30).
* **Inter-VLAN Routing:** Configuring the CORE-RTR01 router to handle routing between all segments.
* **Incident Response:** Diagnosing and resolving a connectivity loss incident caused by an interface shutdown.
* **Proactive Defense:** Implementing a separate Management VLAN (99) and configuring **SNMP/Syslog** alerts for state monitoring.

---

## 🛠️ Infrastructure and Configuration Baseline

### Device Inventory and VLAN Summary

The network utilizes a **Core Router (CORE-RTR01)** to serve as the gateway for all segmented VLANs.

| VLAN ID | Department | Subnet | Gateway |
| :--- | :--- | :--- | :--- |
| **10** | Admin | 10.10.10.0/24 | 10.10.10.1 |
| **20** | Operations | 10.10.20.0/24 | 10.10.20.1 |
| **30** | Security | 10.10.30.0/24 | 10.10.30.1 |
| **99** | Management (OOB) | N/A | N/A |

### Change Implementation: Management VLAN 99

A separate Management VLAN (99) was implemented for out-of-band SNMP/Syslog traffic to enhance security and network isolation.

* **Date:** 10/21/2025
* **Change:** Added Management VLAN 99 for SNMP/Syslog traffic.
* **Verification:** Verified successful pings to the new gateway interface.

---

## 🚨 Incident Response and Troubleshooting

### Incident Summary (NOC-2025-001)

A loss of connectivity was reported between the Admin VLAN (10) and the Operations VLAN (20).

* **Problem:** Ping requests from PC-ADMIN (`10.10.10.24`) to PC-OPS (`10.10.20.24`) failed entirely.
* **Root Cause:** Router sub-interface **`Gig0/0.20`** (serving the Operations VLAN) was found to be **administratively down**.
* **Verification Evidence:**  (Shows 100% packet loss)

### Resolution

| Action Taken | Outcome |
| :--- | :--- |
| **Fix** | Executed `no shutdown` on interface `Gig0/0.20`. |
| **Resolution Verification** | Confirmed successful pings between VLANs 10, 20, and 30, restoring inter-VLAN routing. |

---

## 🚀 Next Steps (Ongoing Project)

This project is ongoing. The next phase will focus on implementing security and redundancy measures across the network perimeter and internal segments.

| Priority | Task | Focus Area |
| :--- | :--- | :--- |
| **1. Security Hardening** | **ACL Implementation:** Configure **Standard and Extended ACLs** on the CORE-RTR01 to restrict traffic (e.g., block PC-OPS from accessing the Security VLAN 30 gateway). | Network Segmentation |
| **2. Monitoring** | **SNMP/Syslog Integration:** Configure **SNMP traps** and **Syslog logging** to send all interface state changes (up/down) and access violation alerts to the NOC-SRV01 server (VLAN 10). | Proactive Defense |
| **3. Resilience** | **FHRP Implementation:** Configure a **First Hop Redundancy Protocol (HSRP/VRRP)** between the CORE-RTR01 and a simulated secondary router to prevent single points of failure. | High Availability |

***

