# Incident Report IR-001

## Incident Title

Network Reconnaissance and Service Enumeration using Nmap

---

# Incident Information

| Field | Value |
|--------|-------|
| Incident ID | IR-001 |
| Date | July 2026 |
| Severity | Medium |
| Status | Investigated |
| Analyst | Akbar Md |
| Detection Source | Splunk Enterprise + Sysmon |

---

# Executive Summary

During Phase 6 of the SOC Home Lab, reconnaissance activity was simulated from the Kali Linux attacker machine against the Windows SOC endpoint. Multiple Nmap scanning techniques were used to identify live hosts, enumerate open ports, detect running services, identify the operating system, and collect network information.

The reconnaissance activity successfully generated network telemetry that was ingested into Splunk Enterprise through Sysmon. The collected events demonstrate how early-stage attacker behavior can be detected before exploitation occurs.

---

# Incident Timeline

| Time | Activity |
|------|----------|
| T0 | Network connectivity verified |
| T1 | ICMP Ping Test |
| T2 | Host Discovery Scan |
| T3 | TCP SYN Port Scan |
| T4 | Service Version Detection |
| T5 | Operating System Detection |
| T6 | Aggressive Scan |
| T7 | Splunk Detection |
| T8 | Investigation Completed |

---

# Source

## Attacker

| Field | Value |
|-------|-------|
| Host | Kali-SOC |
| Operating System | Kali Linux |
| IP Address | 10.10.10.20 |

---

# Target

## Victim

| Field | Value |
|-------|-------|
| Host | WINDOWS-SOC |
| Operating System | Windows 11 |
| IP Address | 10.10.10.30 |

---

# Attack Description

The attacker initiated network reconnaissance by verifying connectivity to the target system using ICMP.

After confirming reachability, Nmap was used to perform several reconnaissance techniques including:

- Host Discovery
- TCP SYN Scan
- Service Version Detection
- Operating System Detection
- Aggressive Enumeration

The objective was to identify exposed services and gather information that could be used during later attack stages.

All activity occurred inside the isolated SOC laboratory environment.

---

# Commands Executed

## ICMP Connectivity

```bash
ping 10.10.10.30
```

---

## Host Discovery

```bash
sudo nmap -sn 10.10.10.0/24
```

---

## SYN Scan

```bash
sudo nmap -sS 10.10.10.30
```

---

## Service Detection

```bash
sudo nmap -sV 10.10.10.30
```

---

## Operating System Detection

```bash
sudo nmap -O 10.10.10.30
```

---

## Aggressive Scan

```bash
sudo nmap -A 10.10.10.30
```

---

# Evidence Collected

The following evidence was collected during the investigation:

- Ping connectivity results
- Host discovery scan
- SYN port scan
- Service enumeration
- OS detection
- Aggressive scan output
- Splunk search results
- Sysmon network events

---

# Open Ports Identified

| Port | Protocol | Service |
|------|----------|----------|
| 135 | TCP | RPC Endpoint Mapper |
| 139 | TCP | NetBIOS Session Service |
| 445 | TCP | Microsoft SMB |
| Additional ports | Observed during scan | Windows Services |

---

# Indicators of Compromise (IOCs)

## Source IP

```
10.10.10.20
```

## Destination IP

```
10.10.10.30
```

## Tool

```
Nmap
```

## Activity

- Host Discovery
- TCP SYN Scan
- Service Enumeration
- OS Detection
- Network Reconnaissance

---

# MITRE ATT&CK Mapping

| Technique | ID |
|------------|----|
| Active Scanning | T1595 |
| Remote System Discovery | T1018 |
| Network Service Scanning | T1046 |

---

# Splunk Detection Queries

## Network Connections

```spl
index=sysmon EventCode=3
```

---

## Event Statistics

```spl
index=sysmon
| stats count by EventCode
```

---

## Network Activity

```spl
index=sysmon EventCode=3
| table _time Image SourceIp DestinationIp DestinationPort
```

---

## Port Scan Detection

```spl
index=sysmon EventCode=3
| stats dc(DestinationPort) as UniquePorts values(DestinationPort) as Ports by SourceIp
| where UniquePorts > 10
```

---

# Investigation Findings

The investigation confirmed that the attacker successfully performed reconnaissance against the Windows endpoint.

Observed activities included:

- Network reachability testing
- Discovery of live hosts
- Enumeration of open TCP ports
- Service identification
- Operating system fingerprinting

Splunk Enterprise successfully ingested the generated Sysmon telemetry, enabling the analyst to identify reconnaissance activity before any exploitation attempts.

---

# Response Actions

- Reviewed network telemetry in Splunk.
- Correlated Sysmon Event ID 3 records.
- Identified the attacking host.
- Verified destination services.
- Documented reconnaissance techniques.
- Continued monitoring for follow-up attack stages.

---

# Lessons Learned

- Network reconnaissance is often the first observable stage of an attack.
- Host-based telemetry provides valuable visibility into network activity.
- Port scanning can be detected by identifying connections to multiple destination ports within a short period.
- Splunk correlation searches significantly improve early detection of reconnaissance behavior.

---

# Conclusion

The simulated reconnaissance activity successfully demonstrated how attackers gather information before exploitation.

The SOC monitoring infrastructure successfully collected and indexed the generated telemetry, enabling rapid investigation and validation of reconnaissance techniques.

This incident confirms that the deployed Splunk Enterprise and Sysmon configuration can effectively detect early-stage attacker behavior within the SOC Home Lab.