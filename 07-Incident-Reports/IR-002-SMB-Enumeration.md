# Incident Report IR-002

## Incident Title

SMB Enumeration and Administrative Authentication Attempt

---

# Incident Information

| Field | Value |
|--------|-------|
| Incident ID | IR-002 |
| Date | July 2026 |
| Severity | Medium |
| Status | Investigated |
| Analyst | Akbar Md |
| Detection Source | Splunk Enterprise + Sysmon |

---

# Executive Summary

During routine attack simulation, the Kali Linux attacker system performed SMB enumeration against the Windows SOC endpoint. Authentication was successfully established using valid local administrator credentials. Administrative shares were enumerated and an authenticated PsExec remote execution attempt was observed.

The activity generated multiple Sysmon network events and Windows authentication events, allowing successful detection inside Splunk Enterprise.

---

# Timeline

| Time | Activity |
|------|----------|
| T0 | Host discovery |
| T1 | TCP SYN Scan |
| T2 | Service Detection |
| T3 | SMB Enumeration |
| T4 | SMB Authentication |
| T5 | Share Enumeration |
| T6 | Administrative Verification |
| T7 | PsExec Execution Attempt |
| T8 | Splunk Detection |

---

# Source

**Attacker**

- Host: Kali Linux
- IP: 10.10.10.20

---

# Target

**Victim**

- Host: Windows-SOC
- IP: 10.10.10.30

---

# Attack Description

The attacker first identified active hosts using ICMP discovery before performing TCP service enumeration using Nmap. SMB services were identified and further enumerated using SMB NSE scripts and NetExec.

Valid credentials were used to authenticate to the target over SMB. Administrative shares were successfully enumerated and administrative privileges were confirmed. A remote execution attempt using Impacket PsExec was initiated. Windows Defender prevented successful interactive execution, however telemetry generated during the attempt was successfully captured by Sysmon.

---

# Evidence Collected

- Nmap scan results
- SMB Enumeration
- NetExec Authentication
- Administrative Share Enumeration
- PsExec Execution Attempt
- Splunk Search Results
- Sysmon Event Logs

---

# Indicators of Compromise

## Source IP

10.10.10.20

## Destination IP

10.10.10.30

## Protocol

SMB (TCP 445)

## Tools

- Nmap
- NetExec
- Impacket PsExec

---

# MITRE ATT&CK Mapping

| Technique | ID |
|------------|----|
| Remote System Discovery | T1018 |
| Network Service Scanning | T1046 |
| Network Share Discovery | T1135 |
| Valid Accounts | T1078 |
| SMB Admin Shares | T1021.002 |
| Service Execution | T1569.002 |

---

# Splunk Detection Queries

Host Discovery

```spl
index=sysmon EventCode=3
```

SMB Authentication

```spl
index=sysmon DestinationPort=445
```

Port Scan Detection

```spl
index=sysmon EventCode=3
| stats dc(DestinationPort) by SourceIp
```

---

# Response Actions

- Verified authentication source.
- Confirmed SMB administrative access.
- Reviewed Sysmon process creation events.
- Validated Windows Defender response.
- Correlated events inside Splunk.

---

# Lessons Learned

- Host-based telemetry provides excellent visibility into SMB activity.
- Administrative authentication should be continuously monitored.
- Network reconnaissance is easily detectable when correlated with Sysmon network events.
- Windows Defender may interrupt offensive tooling while still providing valuable detection opportunities.

---

# Conclusion

The attack simulation successfully demonstrated reconnaissance, SMB authentication, administrative access validation, and attempted remote execution. Splunk Enterprise and Sysmon provided sufficient telemetry to detect and investigate the activity.