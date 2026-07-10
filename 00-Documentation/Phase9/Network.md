# Network Design and Configuration

## Overview

This document describes the network architecture implemented for the SOC Home Lab. The environment was designed to simulate an enterprise network while remaining completely isolated from the production network. The architecture supports attack simulation, centralized logging, threat hunting, and incident response without exposing external systems to generated attack traffic.

---

# Network Objectives

The network was designed to achieve the following objectives:

- Provide Internet connectivity for software installation and updates.
- Isolate attack traffic within the lab environment.
- Allow communication between all virtual machines.
- Support centralized log collection.
- Simulate an enterprise workstation environment.
- Enable safe attack simulations.

---

# Network Topology

```
                         Internet
                             │
                     VMware NAT Network
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
        │                    │                    │
 Ubuntu-SOC             Kali-SOC            Windows-SOC
10.10.10.10           10.10.10.20         10.10.10.30
        │                    │                    │
        └──────── Host-Only SOC Network ──────────┘
```

---

# Network Segments

## VMware NAT Network

Purpose

- Internet access
- Ubuntu package installation
- Windows Updates
- Kali package updates
- Downloading security tools
- GitHub access

Configuration

| Property | Value |
|----------|-------|
| Address Assignment | DHCP |
| Gateway | VMware NAT Gateway |
| DNS | VMware NAT DNS |
| Internet Access | Yes |

---

## SOC Host-Only Network

Purpose

- Attack simulation
- Endpoint communication
- Splunk log forwarding
- Threat hunting
- Detection validation
- Incident response

Configuration

| Property | Value |
|----------|-------|
| Network | 10.10.10.0/24 |
| Gateway | None |
| DNS | None |
| Internet Access | No |

This isolated network ensures that attack traffic remains confined to the lab environment.

---

# IP Address Plan

| Host | Role | IP Address |
|------|------|------------|
| Ubuntu-SOC | Splunk Enterprise | 10.10.10.10 |
| Kali-SOC | Attack Platform | 10.10.10.20 |
| Windows-SOC | Endpoint | 10.10.10.30 |

Subnet Mask

```
255.255.255.0
```

---

# Network Adapters

## Ubuntu-SOC

| Adapter | Network | Purpose |
|----------|---------|---------|
| Adapter 1 | NAT | Internet Access |
| Adapter 2 | Host-Only | SOC Network |

---

## Kali-SOC

| Adapter | Network | Purpose |
|----------|---------|---------|
| Adapter 1 | NAT | Internet Access |
| Adapter 2 | Host-Only | Attack Network |

---

## Windows-SOC

| Adapter | Network | Purpose |
|----------|---------|---------|
| Adapter 1 | NAT | Internet Access |
| Adapter 2 | Host-Only | Endpoint Communication |

---

# Communication Matrix

| Source | Destination | Purpose |
|----------|-------------|----------|
| Kali-SOC | Windows-SOC | Attack Simulation |
| Windows-SOC | Ubuntu-SOC | Log Forwarding |
| Kali-SOC | Ubuntu-SOC | SSH / Administration |
| Ubuntu-SOC | Windows-SOC | Splunk Management |

---

# Log Collection Flow

```
Windows Endpoint
       │
       ▼
Sysmon
       │
       ▼
Splunk Universal Forwarder
       │
       ▼
Ubuntu-SOC
       │
       ▼
Splunk Enterprise
```

---

# Attack Traffic Flow

```
Kali Linux
      │
      ▼
Windows Endpoint
      │
      ▼
Sysmon
      │
      ▼
Splunk Enterprise
```

---

# Connectivity Validation

The following tests were performed throughout the project.

## ICMP Connectivity

Commands

```bash
ping 10.10.10.10
ping 10.10.10.20
ping 10.10.10.30
```

Status

✅ Successful

---

## SSH

Ubuntu Server

```bash
ssh socadmin@10.10.10.10
```

Status

✅ Successful

---

## Splunk Web

```
https://10.10.10.10:8000
```

Status

✅ Accessible

---

## Splunk Forwarder

Port

```
9997/TCP
```

Status

✅ Connected

---

## SMB

Port

```
445/TCP
```

Purpose

Attack simulation and administrative testing.

Status

Validated during attack simulations.

---

# Firewall Considerations

The following ports were required during the project:

| Port | Protocol | Purpose |
|------|----------|----------|
| 22 | TCP | SSH |
| 445 | TCP | SMB |
| 8000 | TCP | Splunk Web |
| 8089 | TCP | Splunk Management |
| 9997 | TCP | Splunk Forwarder |

Firewall rules were adjusted only when necessary to support controlled lab activities.

---

# Network Security

The environment was designed with the following security principles:

- Isolated host-only network
- No direct exposure to the Internet for attack traffic
- Controlled communication paths
- Centralized log collection
- VMware snapshots before major changes
- Reproducible network configuration

---

# Validation Checklist

- [x] NAT connectivity verified
- [x] Host-only connectivity verified
- [x] Static IP addresses configured
- [x] Splunk log forwarding operational
- [x] SSH access verified
- [x] Attack traffic contained within the lab
- [x] Network documentation completed

---

# Conclusion

The networking architecture provides a stable and isolated foundation for the SOC Home Lab. By separating Internet connectivity from attack traffic, the design enables realistic enterprise-style security operations while minimizing risk. The dual-network configuration supports attack simulation, centralized logging, and incident response workflows, making it suitable for continuous learning, experimentation, and portfolio demonstration.