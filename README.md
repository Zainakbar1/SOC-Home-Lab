# 🛡️ SOC Home Lab - Attack & Defense Simulation

![Platform](https://img.shields.io/badge/Platform-VMware_Workstation_Pro-blue)
![OS](https://img.shields.io/badge/OS-Windows_11_|_Ubuntu_|_Kali-success)
![Splunk](https://img.shields.io/badge/SIEM-Splunk_Enterprise-orange)
![Status](https://img.shields.io/badge/Project-100%25_Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)

---

# Overview

This project is a production-inspired Security Operations Center (SOC) Home Lab built using VMware Workstation Pro. It simulates real-world enterprise attack and defense scenarios while focusing on:

- Blue Team Operations
- Detection Engineering
- Threat Hunting
- Incident Response
- Digital Forensics
- MITRE ATT&CK Mapping
- Splunk Enterprise Administration
- Windows Endpoint Monitoring
- Sysmon Telemetry
- Attack Simulation

The goal is to create a complete SOC analyst portfolio demonstrating both offensive security techniques and defensive monitoring.

---

# Current Project Status

| Phase | Status |
|---------|--------|
| [Phase 0 – Infrastructure](00-Documentation/Phase0/README.md) | ✅ Complete |
| [Phase 1 – Network Configuration](00-Documentation/Phase1/README.md) | ✅ Complete |
| [Phase 2 – Splunk Enterprise](00-Documentation/Phase2/README.md) | ✅ Complete |
| [Phase 3 – Windows Logging & Sysmon](00-Documentation/Phase3/README.md) | ✅ Complete |
| [Phase 4 – Kali Linux](00-Documentation/Phase4/README.md) | ✅ Complete |
| [Phase 5 – Log Validation](00-Documentation/Phase5/README.md) | ✅ Complete |
| [Phase 6 – Reconnaissance & SMB Enumeration](00-Documentation/Phase6/README.md) | ✅ Complete |
| [Phase 7 – Credential Access & Remote Execution](00-Documentation/Phase7/README.md) | ✅ Complete |
| [Phase 8 – Persistence & Privilege Escalation](00-Documentation/Phase8/README.md) | ✅ Complete |
| [Phase 9 – Detection Engineering & Threat Hunting](00-Documentation/Phase9/README.md) | ✅ Complete |
| [Phase 10 – Incident Response & Final Portfolio](07-Incident-Reports/LessonsLearned/README.md) | ✅ Complete |

**Overall Progress:** **100%**

---

# Lab Architecture

```
                        INTERNET
                            │
                    VMware NAT Network
                            │
          ┌─────────────────┼─────────────────┐
          │                 │                 │
          │                 │                 │
     Ubuntu SOC        Kali Linux        Windows 11
     10.10.10.10       10.10.10.20       10.10.10.30
          │                 │                 │
          └──────── Host-Only SOC Network ───┘
```

---

# Virtual Machines

## Ubuntu SOC Server

- Ubuntu 26.04 LTS
- Splunk Enterprise
- SSH Server
- Syslog Server
- Deployment Server
- Receiving Indexer

---

## Windows 11 Endpoint

- Sysmon
- Splunk Universal Forwarder
- Windows Event Logging
- Endpoint Telemetry

---

## Kali Linux

Offensive Security Platform containing:

- Nmap
- NetExec
- Impacket
- Hydra
- Metasploit Framework
- Burp Suite
- Gobuster
- SMB Client

---

# VMware Specifications

## Ubuntu SOC

| Setting | Value |
|----------|-------|
| Name | Ubuntu-SOC |
| vCPU | 4 |
| RAM | 12 GB |
| Disk | 80 GB |
| Network | NAT + Host Only |
| Firmware | UEFI |

---

## Windows 11

| Setting | Value |
|----------|-------|
| vCPU | 4 |
| RAM | 8 GB |
| Disk | 80 GB |
| Network | NAT + Host Only |

---

## Kali Linux

| Setting | Value |
|----------|-------|
| vCPU | 4 |
| RAM | 8 GB |
| Disk | 40 GB |
| Network | NAT + Host Only |

---

# Network Plan

| Machine | NAT | SOC Network |
|----------|-----|-------------|
| Ubuntu SOC | DHCP | 10.10.10.10/24 |
| Kali Linux | DHCP | 10.10.10.20/24 |
| Windows 11 | DHCP | 10.10.10.30/24 |

Host-only Network:

```
10.10.10.0/24
```

Gateway:

```
None
```

DNS:

```
None
```

The host-only network isolates attack traffic while allowing controlled communication between lab machines.

---

# Project Structure

```
SOC-LAB/
│
├── 00-Documentation
│   ├── README.md
│   ├── Network_Diagram.drawio
│   ├── IP_Addressing.xlsx
│   ├── Phase0
│   ├── Phase1
│   ├── Phase2
│   ├── Phase3
│   ├── Phase4
│   ├── Phase5
│   ├── Phase6
│   ├── Phase7
│   ├── Phase8
│   ├── Phase9
│   └── Screenshots
│
├── 01-ISO
├── 02-VMs
├── 03-Splunk
│   ├── Enterprise
│   ├── Apps
│   ├── Configurations
│   ├── Dashboards
│   └── Forwarders
│
├── 04-Sysmon
├── 05-Attacks
├── 06-Detections
├── 07-Incident-Reports
├── 08-PCAP
├── 09-Tools
├── 10-MITRE
└── Snapshots
```

---

# Implemented Features

## Infrastructure

- VMware Workstation Pro
- Multi-VM Enterprise Network
- Static Host-Only Network
- Snapshot Strategy

## Splunk

- Splunk Enterprise
- Custom Indexes
- Receiving Indexer
- Deployment Server
- Windows TA
- Sysmon TA
- Dashboards

## Endpoint Monitoring

- Sysmon
- Windows Event Logs
- Universal Forwarder
- Network Telemetry
- Process Monitoring

## Attack Simulations

- Host Discovery
- TCP SYN Scan
- Service Enumeration
- OS Detection
- SMB Enumeration
- SMB Authentication
- Share Enumeration
- Administrative Access Validation
- PsExec Remote Execution Attempt

## Detection Engineering

- Host Discovery Detection
- Port Scan Detection
- SMB Detection
- SMB Authentication Detection
- Administrative Share Detection
- PsExec Detection
- Network Connection Detection

## Incident Response

- [IR-001 – Nmap Reconnaissance](07-Incident-Reports/IR-001-Nmap-Reconnaissance.md)
- [IR-002 – SMB Enumeration](07-Incident-Reports/IR-002-SMB-Enumeration.md)
- [IR-003 – PsExec Lateral Movement](07-Incident-Reports/IR-003-PsExec-LateralMovement.md)
- [IR-004 – Complete Attack Timeline](07-Incident-Reports/IR-004-Complete-Attack-Timeline.md)
- [IR-005 – Threat Hunting Summary](07-Incident-Reports/IR-005-Threat-Hunting-Summary.md)
- [IR-006 – SMB Lateral Movement](07-Incident-Reports/IR-006-SMB-LateralMovement.md)
- [IR-007 – PsExec Investigation](07-Incident-Reports/IR-007-PsExec-Investigation.md)
- [IR-008 – Final Incident Report](07-Incident-Reports/IR-008-Final-Incident-Report.md)

## MITRE ATT&CK Mapping

- T1018 – Remote System Discovery
- T1046 – Network Service Discovery
- T1135 – Network Share Discovery
- T1078 – Valid Accounts
- T1021.002 – SMB/Windows Admin Shares
- T1569.002 – Service Execution

---

# Snapshot Strategy

| Snapshot | Description |
|-----------|-------------|
| Ubuntu SS1 | Fresh Installation |
| Ubuntu SS2 | Network Configuration |
| Ubuntu SS3 | Splunk + Sysmon Configuration |
| Windows SS1 | Base Installation |
| Windows SS2 | Network Configuration |
| Windows SS3 | Universal Forwarder + Sysmon |
| Kali SS1 | Fresh Installation |
| Kali SS2 | Network Configuration |

Snapshots are created before major configuration changes to provide reliable rollback points.

---

# 📖 Documentation Directory & Quick Links

All phases and components of this project are thoroughly documented. You can access the specific documentation indices, phase guides, configurations, and incident reports directly using the links below:

### 🗺️ Documentation Index
* **[Comprehensive Documentation Index](00-Documentation/README.md)** - General overview of lab network architecture, setup phases, and specifications.

### ⚙️ Phase-by-Phase Walkthroughs
| Phase | Documentation Link | Description |
| :--- | :--- | :--- |
| **Phase 0** | 🛠️ **[Infrastructure Setup](00-Documentation/Phase0/README.md)** | VMware Workstation Pro installation, VM creation (Ubuntu, Windows 11, Kali), and base snapshot strategy. |
| **Phase 1** | 🔌 **[Network Configuration](00-Documentation/Phase1/README.md)** | Host-only isolated networking (10.10.10.0/24), firewall configuration, and connectivity verification. |
| **Phase 2** | 📊 **[Splunk Installation & Config](00-Documentation/Phase2/README.md)** | Installing Splunk Enterprise on Ubuntu, setting up receiving indexers, and creating custom indexes. |
| **Phase 3** | 🎛️ **[Windows Logging & Sysmon](00-Documentation/Phase3/README.md)** | Installing Universal Forwarder and Sysmon on Win 11, configuring forwarding inputs. |
| **Phase 4** | 🕵️ **[Kali Linux & Reconnaissance](00-Documentation/Phase4/README.md)** | Setting up the Kali attacker machine and executing initial Nmap scans. |
| **Phase 5** | ✅ **[Log Validation & TAs](00-Documentation/Phase5/README.md)** | Configuring Splunk Technology Add-ons (TAs) to parse Windows/Sysmon logs. |
| **Phase 6** | 🔍 **[SMB Reconnaissance & Enumeration](00-Documentation/Phase6/README.md)** | Adversary discovery techniques, SMB share scanning, NetExec usage, and PsExec execution attempts. |
| **Phase 7** | 🔓 **[Credential Access & Remote Execution](00-Documentation/Phase7/README.md)** | SMB brute force/password spraying via Hydra, and remote code execution with Impacket-PsExec. |
| **Phase 8** | ☠️ **[Persistence & Privilege Escalation](00-Documentation/Phase8/README.md)** | Simulating Registry run keys, scheduled tasks, privilege escalation, and active threat hunting. |
| **Phase 9** | 🎯 **[Detection Engineering & Splunk](00-Documentation/Phase9/README.md)** | Writing custom Splunk SPL detection rules for each simulated attack technique. |
| **Phase 10** | 📝 **[Lessons Learned & Incident Reports](07-Incident-Reports/LessonsLearned/README.md)** | Final incident response lifecycle summary, post-incident reviews, and lessons learned. |

### 🛠️ Configuration & Core Component Readmes
* 💻 **[Sysmon Configuration](04-Sysmon/README.md)** - Details on custom Sysmon XML schema and event definitions.
* 📦 **[Splunk Apps Config](03-Splunk/Apps/README.md)** - Installed apps, addons, and indexes.
* ⚙️ **[Splunk System Configurations](03-Splunk/Configurations/README.md)** - Splunk config files (`inputs.conf`, `outputs.conf`, `server.conf`).
* 📊 **[Splunk Dashboards](03-Splunk/Dashboards/README.md)** - Visualizations, security monitoring dashboards, and XML exports.
* 🗺️ **[MITRE ATT&CK Mapping Reference](10-MITRE/README.md)** - Full tactic & technique coverage tracker.
* 💾 **[VMware Snapshot Guide](Snapshots/README.md)** - Lab rollback points and snapshot topology.
* 🔧 **[Splunk Scripts & Tools](09-Tools/Splunk/README.md)** - Helper scripts and log generation utilities.

### ⚔️ Adversary Simulations & Detections
* 🏹 **[Phase 8 Offensive Playbook](05-Attacks/Phase8/README.md)** - Complete persistence, discovery, and escalation details.
  * 📡 **[Discovery Simulations](05-Attacks/Phase8/Discovery/README.md)**
  * 📌 **[Persistence Simulations](05-Attacks/Phase8/Persistence/README.md)** (See also **[Phase 7 Persistence](05-Attacks/Phase7/Persistence/README.md)**)
  * 🎯 **[Threat Hunting Strategies](05-Attacks/Phase8/ThreatHunting/README.md)**
  * ⏳ **[Attack Timeline](05-Attacks/Phase8/Timeline/README.md)**
* 🛡️ **[Detection Rules Index](06-Detections/README.md)** - Core detection queries and alerts.
  * 🔔 **[Phase 8 Detections](06-Detections/Phase8/README.md)**

---

# Technologies Used

- VMware Workstation Pro
- Ubuntu Server/Desktop
- Windows 11
- Kali Linux
- Splunk Enterprise
- Sysmon
- Splunk Universal Forwarder
- Nmap
- NetExec
- Impacket
- Metasploit
- Hydra
- Burp Suite
- Gobuster

---

# Upcoming Phases

- Credential Access
- Remote Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Threat Hunting
- Detection Engineering
- Incident Response
- Dashboard Development
- Final SOC Portfolio

---

# Author

**Akbar Md**

Bachelor of Technology – Internet of Things

SOC Analyst | Blue Team | Detection Engineering | Threat Hunting | Splunk | Windows Security | Cybersecurity

---

⭐ **If you find this project useful, consider starring the repository.**