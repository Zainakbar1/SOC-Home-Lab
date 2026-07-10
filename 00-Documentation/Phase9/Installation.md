# Installation Guide

## Overview

This document provides a complete installation guide for recreating the SOC Home Lab from a clean Windows host. Following these steps will result in a fully functional enterprise-style Security Operations Center (SOC) environment capable of attack simulation, centralized logging, detection engineering, threat hunting, and incident response.

---

# Hardware Requirements

## Minimum

| Component | Requirement |
|------------|-------------|
| CPU | 6 Core Processor |
| RAM | 24 GB |
| Storage | 300 GB SSD |
| Virtualization | AMD-V / Intel VT-x |

---

## Recommended

| Component | Requirement |
|------------|-------------|
| CPU | AMD Ryzen 7 / Intel Core i7 or better |
| RAM | 40 GB |
| Storage | 512 GB NVMe SSD |
| GPU | Optional |

---

# Host Operating System

- Windows 11 Pro (64-bit)

---

# Software Requirements

| Software | Purpose |
|----------|---------|
| VMware Workstation Pro | Virtualization |
| Ubuntu 26.04 LTS ISO | SOC Server |
| Windows 11 ISO | Endpoint |
| Kali Linux ISO | Attack Platform |
| Splunk Enterprise | SIEM |
| Sysmon | Endpoint Telemetry |
| Splunk Universal Forwarder | Log Collection |

---

# Lab Architecture

```
                         Internet
                             │
                     VMware NAT Network
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
 Ubuntu-SOC             Kali-SOC            Windows-SOC
10.10.10.10           10.10.10.20         10.10.10.30
        │                    │                    │
        └──────── Host-Only SOC Network ──────────┘
```

---

# Installation Workflow

The lab should be built in the following order:

```
VMware Installation
        │
        ▼
Download ISOs
        │
        ▼
Create Virtual Networks
        │
        ▼
Ubuntu Installation
        │
        ▼
Splunk Installation
        │
        ▼
Windows Installation
        │
        ▼
Sysmon Installation
        │
        ▼
Splunk Forwarder
        │
        ▼
Kali Installation
        │
        ▼
Attack Simulation
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

# Phase Installation Order

| Phase | Description | Status |
|--------|-------------|--------|
| Phase 0 | Planning & VMware Setup | ✅ |
| Phase 1 | Ubuntu SOC Server | ✅ |
| Phase 2 | Splunk Enterprise | ✅ |
| Phase 3 | Windows Logging | ✅ |
| Phase 4 | Kali Linux | ✅ |
| Phase 5 | Attack Simulation | ✅ |
| Phase 6 | Detection Engineering | ✅ |
| Phase 7 | Threat Hunting | ✅ |
| Phase 8 | Incident Response | ✅ |
| Phase 9 | Documentation | ✅ |

---

# Virtual Machine Configuration

## Ubuntu-SOC

| Setting | Value |
|----------|-------|
| CPU | 4 vCPU |
| RAM | 12 GB |
| Disk | 80 GB |
| Adapter 1 | NAT |
| Adapter 2 | Host-Only |

---

## Windows-SOC

| Setting | Value |
|----------|-------|
| CPU | 4 vCPU |
| RAM | 8 GB |
| Disk | 80 GB |
| Adapter 1 | NAT |
| Adapter 2 | Host-Only |

---

## Kali-SOC

| Setting | Value |
|----------|-------|
| CPU | 4 vCPU |
| RAM | 8 GB |
| Disk | 40 GB |
| Adapter 1 | NAT |
| Adapter 2 | Host-Only |

---

# Network Configuration

## Host-Only Network

| Host | IP Address |
|------|------------|
| Ubuntu-SOC | 10.10.10.10 |
| Kali-SOC | 10.10.10.20 |
| Windows-SOC | 10.10.10.30 |

Subnet

```
255.255.255.0
```

Gateway

```
None
```

---

# Required Components

## Ubuntu

Install:

- OpenSSH Server
- Splunk Enterprise
- Syslog
- Splunk Apps

---

## Windows

Install:

- Sysmon
- Splunk Universal Forwarder

---

## Kali

Install/Verify:

- Nmap
- Hydra
- Metasploit
- Gobuster
- Burp Suite
- Impacket

---

# Validation Checklist

Verify the following after installation:

## Ubuntu

- [ ] SSH accessible
- [ ] Splunk running
- [ ] Port 8000 available
- [ ] Port 9997 listening

---

## Windows

- [ ] Sysmon installed
- [ ] Splunk Forwarder running
- [ ] Logs visible in Splunk

---

## Kali

- [ ] Connectivity verified
- [ ] Required tools installed
- [ ] Attack simulations operational

---

# VMware Snapshot Strategy

Create snapshots after each milestone:

| Snapshot | Description |
|-----------|-------------|
| Snapshot 01 | Fresh Installation |
| Snapshot 02 | Ubuntu Configured |
| Snapshot 03 | Splunk Installed |
| Snapshot 04 | Windows Ready |
| Snapshot 05 | Sysmon Configured |
| Snapshot 06 | Kali Ready |
| Snapshot 07 | Complete SOC Lab |

---

# Repository Structure

```
SOC-LAB/
│
├──00-Documentation/
├──01-ISO/
├──02-VMs/
├──03-Splunk/
├──04-Sysmon/
├──05-Attacks/
├──06-Detections/
├──07-Incident-Reports/
├──08-PCAP/
├──09-Tools/
└──Snapshots/
```

---

# Final Validation

Before using the lab, verify:

- VMware networking is operational.
- All virtual machines communicate on the Host-Only network.
- Internet access works through NAT.
- Splunk receives Sysmon logs.
- Detection queries execute successfully.
- Threat hunting workflows return expected telemetry.
- Incident response documentation aligns with generated evidence.

---

# Outcome

Following this installation guide results in a fully operational SOC Home Lab capable of demonstrating practical cybersecurity skills including SIEM administration, endpoint telemetry collection, detection engineering, threat hunting, incident response, and MITRE ATT&CK mapping. The environment is reproducible, isolated, and suitable for learning, research, and professional portfolio presentation.