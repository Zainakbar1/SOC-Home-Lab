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

![Ping Windows Before Attack](../Screenshots/Phase6/01-ping-windows-before-attack.png)
*Figure 1: Verification of network reachability to the target Windows host.*

## Host Discovery

```bash
sudo nmap -sn 10.10.10.0/24
```

![Host Discovery Scan](../Screenshots/Phase6/02-host-discovery-scan.png)
*Figure 2: Discovering active endpoints in the SOC-LAB subnet using Nmap.*

## SYN Scan

```bash
sudo nmap -sS 10.10.10.30
```

![SYN Port Scan](../Screenshots/Phase6/04-syn-port-scan.png)
*Figure 4: Nmap SYN stealth scan identifying open ports on the target.*

## Service Detection

```bash
sudo nmap -sV 10.10.10.30
```

![Service Version Scan](../Screenshots/Phase6/05-service-version-scan.png)
*Figure 5: Nmap service version detection scan.*

## Aggressive Scan

```bash
sudo nmap -A 10.10.10.30
```

![Aggressive Scan](../Screenshots/Phase6/06-aggressive-scan.png)
*Figure 6: Nmap aggressive scan output.*

## SMB Enumeration

```bash
sudo nmap --script smb-enum-shares 10.10.10.30
```

![Ping Before SMB Enumeration](../Screenshots/Phase6/10-ping-before-smb-enumeration.png)
*Figure 10: Connectivity verification before starting SMB scans.*

![SMB Share Enumeration with Nmap](../Screenshots/Phase6/11-smb-enumeration.png)
*Figure 11: Nmap SMB enumeration script running against the Windows VM.*

## SMB Security Mode

```bash
sudo nmap --script smb-security-mode 10.10.10.30
```

![SMB Security Mode](../Screenshots/Phase6/12-smb-security-mode.png)
*Figure 12: Checking SMB security configurations (signing required/optional).*

## SMB Protocol Discovery

```bash
sudo nmap --script smb-protocols 10.10.10.30
```

![SMB Protocol Discovery](../Screenshots/Phase6/13-smb-protocols.png)
*Figure 13: Verifying supported SMB dialects on the target.*

![SMB2 Security Mode](../Screenshots/Phase6/14-smb2-security-mode.png)
*Figure 14: Checking SMBv2 security settings.*

## SMB Authentication

```bash
netexec smb 10.10.10.30 -u socadmin -p root
```

![Attack Tools Installed](../Screenshots/Phase6/16-attack-tools-installed.png)
*Figure 16: Attacker toolkit environment setup verification on Kali.*

![SMB Authentication Success](../Screenshots/Phase6/17-smb-authentication-success.png)
*Figure 17: NetExec validating administrative user login over SMB.*

## SMB Share Enumeration

```bash
netexec smb 10.10.10.30 -u socadmin -p root --shares
```

![SMB Share Enumeration](../Screenshots/Phase6/18-smb-share-enumeration.png)
*Figure 18: Administrative share discovery using NetExec.*

## Administrative Verification

```bash
netexec smb 10.10.10.30 -u socadmin -p root --local-auth
```

![Local Administrators Group](../Screenshots/Phase6/19-local-administrators-group.png)
*Figure 19: Local administrators group lookup on target endpoint.*

![Enable LocalAccountTokenFilterPolicy](../Screenshots/Phase6/20-enable-localaccounttokenfilterpolicy.png)
*Figure 20: Enabling token filter policy for local administrative access.*

![NetExec Local Admin Pwn3d](../Screenshots/Phase6/21-netexec-local-admin-pwn3d.png)
*Figure 21: Successful authentication showing (Pwn3d!) signifying full administrative access.*

## Remote Execution Attempt

```bash
impacket-psexec WINDOWS-SOC/socadmin:root@10.10.10.30
```

![Impacket PsExec Attempt](../Screenshots/Phase6/22-impacket-psexec-attempt.png)
*Figure 22: Attacking endpoint using impacket-psexec.*

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

![Splunk Search After Host Discovery](../Screenshots/Phase6/03-splunk-search-after-host-discovery.png)
*Figure 3: Splunk search confirming host discovery event ingestion.*

![EventCode Statistics](../Screenshots/Phase6/07-eventcode-statistics.png)
*Figure 7: Statistics of received EventCodes in Splunk.*

![Network Connection Events](../Screenshots/Phase6/08-network-connection-events.png)
*Figure 8: Sysmon network connection events generated by the port scans.*

![PortScan Detection Query](../Screenshots/Phase6/09-portscan-detection-query.png)
*Figure 9: Port scan detection query results.*

![Splunk After SMB Enumeration](../Screenshots/Phase6/15-splunk-after-smb-enumeration.png)
*Figure 15: Splunk search results displaying SMB activity logs.*

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