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
| Phase 0 – Infrastructure | ✅ Complete |
| Phase 1 – Network Configuration | ✅ Complete |
| Phase 2 – Splunk Enterprise | ✅ Complete |
| Phase 3 – Windows Logging & Sysmon | ✅ Complete |
| Phase 4 – Kali Linux | ✅ Complete |
| Phase 5 – Log Validation | ✅ Complete |
| Phase 6 – Reconnaissance & SMB Enumeration | ✅ Complete |
| Phase 7 – Credential Access & Remote Execution | ✅ Complete |
| Phase 8 – Persistence & Privilege Escalation | ✅ Complete |
| Phase 9 – Detection Engineering & Threat Hunting | ✅ Complete |
| Phase 10 – Incident Response & Final Portfolio | ✅ Complete |

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

- IR-001 – Nmap Reconnaissance
- IR-002 – SMB Enumeration

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

# Documentation

Every phase includes:

- Detailed README
- Commands Executed
- Technical Explanations
- Screenshots
- Detection Queries
- MITRE Mapping
- Incident Reports
- Lessons Learned

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