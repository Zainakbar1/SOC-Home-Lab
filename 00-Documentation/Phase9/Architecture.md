# SOC Home Lab Architecture

## Overview

This document describes the architecture of the SOC Home Lab, including the virtualization environment, network design, system roles, and communication flow. The objective of the architecture is to provide an isolated enterprise-style environment for practicing attack simulation, detection engineering, threat hunting, and incident response.

---

# High-Level Architecture

```
                         Internet
                             │
                     VMware NAT Network
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
        │                    │                    │
  Ubuntu SOC             Kali Linux          Windows 11
  10.10.10.10            10.10.10.20         10.10.10.30
        │                    │                    │
        └────────── Host-Only SOC Network ───────┘
```

---

# Virtual Machines

## Ubuntu-SOC

Role:

- Splunk Enterprise Server
- Centralized Log Collection
- Universal Forwarder Management
- SSH Server
- Syslog Server

Specifications

| Component | Value |
|-----------|-------|
| Operating System | Ubuntu 26.04 LTS |
| CPU | 4 vCPU |
| RAM | 12 GB |
| Disk | 80 GB |
| Adapter 1 | NAT |
| Adapter 2 | Host Only |

---

## Kali-SOC

Role

- Attack Simulation
- Vulnerability Assessment
- Enumeration
- Lateral Movement Simulation

Installed Tools

- Nmap
- Metasploit Framework
- Hydra
- Burp Suite
- Gobuster
- Impacket

Specifications

| Component | Value |
|-----------|-------|
| CPU | 4 vCPU |
| RAM | 8 GB |
| Disk | 40 GB |
| Adapter 1 | NAT |
| Adapter 2 | Host Only |

---

## Windows-SOC

Role

- Victim Workstation
- Endpoint Telemetry
- Detection Validation

Installed Components

- Sysmon
- Splunk Universal Forwarder
- Windows Defender

Specifications

| Component | Value |
|-----------|-------|
| CPU | 4 vCPU |
| RAM | 8 GB |
| Disk | 80 GB |
| Adapter 1 | NAT |
| Adapter 2 | Host Only |

---

# Network Architecture

## NAT Network

Purpose

- Internet access
- Software installation
- System updates
- Package downloads

Configuration

```
Address Assignment: DHCP
Gateway: VMware NAT
DNS: VMware NAT
```

---

## Host-Only SOC Network

Purpose

- Attack simulation
- Log collection
- Isolated communication
- Threat hunting
- Detection validation

Configuration

| Device | IP Address |
|---------|------------|
| Ubuntu-SOC | 10.10.10.10 |
| Kali-SOC | 10.10.10.20 |
| Windows-SOC | 10.10.10.30 |

Network

```
10.10.10.0/24
```

Gateway

```
None
```

DNS

```
None
```

---

# Log Flow

```
Windows Sysmon
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Enterprise
        │
        ▼
Detection Engineering
        │
        ▼
Threat Hunting
        │
        ▼
Incident Response
```

---

# Attack Flow

```
Kali Linux
      │
      ▼
Discovery
      │
      ▼
Enumeration
      │
      ▼
Persistence
      │
      ▼
Remote Execution
      │
      ▼
Telemetry Generation
```

---

# Defensive Workflow

```
Sysmon
     │
     ▼
Splunk
     │
     ▼
Detection Rules
     │
     ▼
Threat Hunting
     │
     ▼
IOC Analysis
     │
     ▼
Incident Response
```

---

# Security Components

| Component | Function |
|------------|----------|
| VMware Workstation Pro | Virtualization |
| Ubuntu Server | SIEM Platform |
| Splunk Enterprise | Log Analysis |
| Splunk Universal Forwarder | Log Collection |
| Sysmon | Endpoint Telemetry |
| Windows Defender | Endpoint Protection |
| Kali Linux | Attack Simulation |

---

# MITRE ATT&CK Coverage

The architecture supports validation of the following ATT&CK tactics:

- Discovery
- Execution
- Persistence
- Defense Evasion
- Credential Access (future expansion)
- Lateral Movement
- Collection
- Command and Control (future expansion)

---

# Design Principles

The lab was designed using the following principles:

- **Isolation:** All attack traffic remains within the host-only network.
- **Reproducibility:** Every phase can be recreated from documented steps.
- **Scalability:** Additional endpoints, servers, and tools can be added without redesigning the network.
- **Observability:** Sysmon and Splunk provide centralized visibility into endpoint activity.
- **Security:** The lab is separated from the production network and uses snapshots for safe experimentation.

---

# Future Enhancements

Potential improvements include:

- Active Directory Domain Controller
- Windows Server
- Microsoft Sysmon Event ID tuning
- Splunk Enterprise Security (ES)
- Zeek Network Security Monitor
- Suricata IDS
- Wazuh Integration
- Velociraptor DFIR
- TheHive and Cortex
- MISP Threat Intelligence

---

# Architecture Summary

The SOC Home Lab provides a production-inspired environment for blue-team training. The architecture combines VMware virtualization, Windows endpoint telemetry, Splunk SIEM, and Kali-based attack simulation to create an end-to-end workflow for detection engineering, threat hunting, and incident response. The modular design allows future expansion while maintaining a secure and isolated environment suitable for cybersecurity research and portfolio development.