# Port Scanning

## Overview

Following successful host discovery, a TCP port scan was performed against the Windows endpoint using Nmap. The purpose of this activity was to identify accessible services and verify which ports could be used during later attack simulations.

Port scanning is one of the most common reconnaissance techniques used by attackers to identify exposed services and potential attack vectors.

---

# Objective

- Identify open TCP ports
- Discover running network services
- Verify SMB accessibility
- Generate telemetry for detection validation

---

# Environment

| Component | Value |
|-----------|-------|
| Attacker | Kali-SOC |
| Target | Windows-SOC |
| Attacker IP | 10.10.10.20 |
| Target IP | 10.10.10.30 |
| Tool | Nmap |

---

# MITRE ATT&CK

| Tactic | Technique |
|--------|-----------|
| Discovery | T1046 – Network Service Discovery |

---

# Commands Executed

## Basic TCP Scan

```bash
nmap -Pn 10.10.10.30
```

## Service Detection

```bash
nmap -sV 10.10.10.30
```

## SMB Port Scan

```bash
nmap -Pn -p445 10.10.10.30
```

---

# Expected Result

- Target reachable
- Open ports identified
- SMB service detected
- Service versions identified where possible

---

# Actual Result

The scan successfully identified active network services on the Windows endpoint. Port 445 (SMB) was confirmed to be open, enabling subsequent SMB enumeration and remote administration simulations.

---

# Detection Opportunities

This activity may generate indicators including:

- Multiple connection attempts
- Sequential TCP port probes
- SMB service discovery
- Network scanning behavior

Potential detections include:

- Nmap scan detection
- High-rate connection monitoring
- Network service discovery alerts

---

# Evidence

Related screenshots:

- Phase7-01 – Nmap Service Verification
- Phase7-03 – SMB Port Verification

---

# Follow-up Activities

Successful port scanning enabled:

- Service Enumeration
- SMB Enumeration
- Share Enumeration
- PsExec Remote Execution
- Threat Hunting Validation

---

# Outcome

Port scanning successfully identified the services exposed by the Windows endpoint and confirmed SMB availability. The information gathered during this phase was used to guide later attack simulations and validate detection engineering workflows within Splunk Enterprise.