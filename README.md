# Wazuh SIEM Deployment — Multi-Endpoint Security Monitoring

**ITSimplera Institute — Blue Team Internship Program**
**Week 1 Task | Setup + Exploration | Submitted by Muzaker Khan**

---

## Overview

This project deploys a centralized Wazuh SIEM environment across three virtual machines: a Kali Linux manager running the full Wazuh stack (indexer, manager, Filebeat, dashboard), a Windows 10 endpoint enrolled as a Wazuh agent, and a second, independent Kali Linux endpoint also enrolled as a Wazuh agent. File Integrity Monitoring (FIM) was configured and validated on the Linux agent, and live security events were verified end-to-end through the Wazuh dashboard.

The task also involved diagnosing and resolving a real agent/manager version-mismatch failure — documented in full in the report, including root cause and fix.

## Architecture

| Component | Role | OS | IP Address | Wazuh Version |
|---|---|---|---|---|
| Manager | Server + Dashboard | Kali Linux 2025.4 | `192.168.179.128` | 4.7.5 → upgraded to 4.14.6 |
| Windows Agent | Endpoint (`win10`, ID 001) | Windows 10 | `192.168.179.142` | 4.14.5 |
| Linux Agent | Endpoint (`klin`, ID 002) | Kali Linux | `192.168.179.143` | 4.14.6 |

All three VMs run under VMware Workstation on a shared NAT subnet (`192.168.179.0/24`).

## What Was Done

- Deployed the Wazuh manager stack (indexer, manager, Filebeat, dashboard) via the official install script
- Installed and registered the Wazuh agent on a Windows 10 endpoint (MSI installer)
- Installed and registered the Wazuh agent on a separate Kali Linux endpoint (APT)
- Diagnosed and fixed an agent/manager version-mismatch connection failure by upgrading the manager stack in place
- Configured real-time File Integrity Monitoring (Syscheck) on the Linux agent, monitoring `/home`
- Validated FIM by creating/modifying a test file and confirming `added`/`modified` alerts in the dashboard
- Verified live security events from the Windows agent via the Wazuh Threat Hunting dashboard, including automatic PCI DSS compliance mapping

## Repository Structure