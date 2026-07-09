# Phase 6 – Reconnaissance & SMB Enumeration

## Overview

Phase 6 focuses on performing reconnaissance and SMB enumeration against the Windows endpoint from the Kali Linux attacker machine. The objective is to simulate the initial reconnaissance phase of an attack while validating that Splunk Enterprise and Sysmon successfully capture and log the generated activity.

This phase introduces offensive reconnaissance techniques and demonstrates how a SOC analyst can identify scanning behavior, SMB authentication attempts, and administrative access attempts using host-based telemetry.

---

# Objectives

- Verify network connectivity
- Discover active hosts
- Identify open ports
- Enumerate network services
- Detect operating system information
- Enumerate SMB services
- Validate SMB authentication
- Enumerate available SMB shares
- Attempt authenticated remote administration
- Validate Sysmon logging
- Verify Splunk detection capability

---

# Lab Topology

| Machine | Operating System | IP Address | Role |
|----------|-----------------|-----------|------|
| Ubuntu SOC | Ubuntu 26.04 | 10.10.10.10 | Splunk Enterprise |
| Kali Linux | Kali Linux | 10.10.10.20 | Attacker |
| Windows SOC | Windows 11 | 10.10.10.30 | Target |

---

# Tools Used

- Nmap
- NetExec
- Impacket PsExec
- SMB Client
- Splunk Enterprise
- Sysmon
- Windows Event Logs

---

# Attack Workflow

1. Verify network connectivity
2. Perform host discovery
3. Execute SYN port scan
4. Perform service detection
5. Execute aggressive scan
6. Enumerate SMB services
7. Identify supported SMB protocols
8. Validate SMB security configuration
9. Authenticate using NetExec
10. Enumerate SMB shares
11. Verify administrative privileges
12. Attempt remote execution using PsExec
13. Validate telemetry in Splunk

---

# Commands Executed

## Ping

```bash
ping 10.10.10.30
```

## Host Discovery

```bash
sudo nmap -sn 10.10.10.0/24
```

## SYN Scan

```bash
sudo nmap -sS 10.10.10.30
```

## Service Detection

```bash
sudo nmap -sV 10.10.10.30
```

## Aggressive Scan

```bash
sudo nmap -A 10.10.10.30
```

## SMB Enumeration

```bash
sudo nmap --script smb-enum-shares 10.10.10.30
```

## SMB Security Mode

```bash
sudo nmap --script smb-security-mode 10.10.10.30
```

## SMB Protocol Discovery

```bash
sudo nmap --script smb-protocols 10.10.10.30
```

## SMB Authentication

```bash
netexec smb 10.10.10.30 -u socadmin -p root
```

## SMB Share Enumeration

```bash
netexec smb 10.10.10.30 -u socadmin -p root --shares
```

## Administrative Verification

```bash
netexec smb 10.10.10.30 -u socadmin -p root --local-auth
```

## Remote Execution Attempt

```bash
impacket-psexec WINDOWS-SOC/socadmin:root@10.10.10.30
```

---

# Splunk Validation

Telemetry was validated using Sysmon process creation and network connection events.

Example searches:

```spl
index=sysmon EventCode=3
```

```spl
index=sysmon EventCode=1
```

```spl
index=sysmon DestinationPort=445
```

---

# MITRE ATT&CK Mapping

| Technique | ID |
|------------|----|
| Remote System Discovery | T1018 |
| Network Service Scanning | T1046 |
| Network Share Discovery | T1135 |
| Valid Accounts | T1078 |
| SMB/Windows Admin Shares | T1021.002 |
| Service Execution | T1569.002 |

---

# Detection Summary

The following activities were successfully detected:

- Host discovery
- Port scanning
- Service enumeration
- SMB authentication
- SMB share enumeration
- Administrative authentication
- PsExec service creation attempt
- Sysmon process creation
- Sysmon network connections

---

# Evidence

Evidence collected during this phase includes:

- Splunk search results
- Sysmon logs
- Nmap scan output
- NetExec authentication
- SMB enumeration
- PsExec execution attempt
- Windows administrative verification

---

# Lessons Learned

- Host-based telemetry provides detailed visibility into attacker activity.
- SMB authentication attempts are easily correlated in Splunk.
- Administrative shares require elevated privileges.
- Windows Defender can interrupt offensive tooling while still generating useful telemetry.
- Reconnaissance generates valuable indicators for SOC analysts.

---

# Screenshots

This phase contains twenty-two screenshots documenting every stage of reconnaissance, enumeration, authentication, and validation.

---

# Phase Status

**Status:** Completed

**Completion:** 100%