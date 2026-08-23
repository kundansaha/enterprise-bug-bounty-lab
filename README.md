# Enterprise-Segmented Bug Bounty & SIEM Lab

## Project Objective
* **The Goal:** Build a self-hosted, offline bug bounty and penetration testing environment with zero external cloud hosting costs.
* **The Solution:** Engineered a strictly segmented network architecture using virtualized infrastructure, isolating vulnerable target machines while maintaining complete visibility via a centralized Security Information and Event Management (SIEM) system.

---

## Network Architecture
* **Hypervisor:** QEMU/KVM on a Linux Mint host machine.
* **Router / Firewall:** pfSense virtual appliance acting as the gateway between subnets.
* **Blue Zone (Monitoring):** Ubuntu Server hosting the centralized Wazuh SIEM Manager (`192.168.10.100`).
* **Red Zone (Vulnerable Targets):** Windows 10 Pro endpoint with Wazuh Agent installed (`192.168.20.100`).
* **Routing & Security Rules:** pfSense configured to drop all outbound internet traffic from the Red Zone while allowing one-way event telemetry to cross over to the Blue Zone on ports 1514/1515.

---

## Technologies Used
* **Wazuh** (SIEM & Threat Detection)
* **pfSense** (Network Segmentation & Firewall Rules)
* **QEMU / KVM** (Virtualization)
* **Windows Event Viewer / Security Telemetry**

---

## Proof of Concept: Detecting Privilege Escalation
* **The Attack Scenario:** Simulated an adversary establishing persistence on the isolated Windows machine by creating a rogue local account and escalating privileges to the `Administrators` group.
* **Forensic Telemetry:** Filtered out system vulnerability noise to isolate the security event logs. Extracted the exact payload details from the raw JSON telemetry, identifying the rogue user (`hacker_backdoor`) and the compromised executing identity (`bunny`).

### Raw Telemetry Evidence
![Wazuh Telemetry Evidence](Screenshot%20from%202026-08-23%2012-12-51.png)
