# Service Enumeration

## Overview

Service Enumeration was performed after identifying active hosts and open ports during the reconnaissance phase. The objective was to determine the services running on the target Windows endpoint, identify their versions where possible, and assess which services could be leveraged during subsequent attack simulations.

This activity provides attackers with valuable information about exposed applications, protocols, and potential attack surfaces.

---

# Objective

- Identify running network services
- Detect service versions
- Verify SMB availability
- Validate attack paths
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

## Service Version Detection

```bash
nmap -sV 10.10.10.30
```

## SMB Version Detection

```bash
nmap --script smb-protocols -p445 10.10.10.30
```

## SMB Security Mode Detection

```bash
nmap --script smb-security-mode -p445 10.10.10.30
```

---

# Expected Result

The scan should:

- Identify active services
- Detect service versions
- Confirm SMB availability
- Verify protocol support

---

# Actual Result

Service enumeration successfully confirmed that the Windows endpoint was exposing SMB over TCP port 445. The collected information validated that the target was suitable for SMB enumeration and remote administration simulations performed later in the project.

---

# Detection Opportunities

Service enumeration activity may generate:

- Repeated connection attempts
- SMB protocol negotiation
- Network discovery events
- Service fingerprinting indicators

These behaviors can be identified through:

- Sysmon Network Connection events
- Firewall logs
- Network IDS/IPS (if deployed)
- Splunk correlation searches

---

# Evidence

Related screenshots:

- Phase7-01 – Nmap Service Verification
- Phase7-03 – SMB Port Verification
- Phase7-07 – NetExec Share Enumeration

---

# Follow-up Activities

The results from service enumeration enabled:

- SMB Enumeration
- Share Enumeration
- Authentication Testing
- PsExec Remote Execution
- Threat Hunting
- Detection Engineering Validation

---

# Defensive Considerations

Defenders should monitor for:

- High-volume service discovery
- Repeated TCP connection attempts
- SMB protocol reconnaissance
- Unusual scanning activity from internal hosts

Possible mitigations include:

- Restrict unnecessary services
- Limit SMB exposure
- Enable endpoint telemetry
- Monitor network scanning behavior
- Create alerts for reconnaissance patterns

---

# Outcome

Service enumeration successfully identified the services exposed by the Windows endpoint and confirmed that SMB was available for controlled attack simulation. The collected information supported subsequent phases of the SOC Home Lab, including lateral movement, detection engineering, threat hunting, and incident response.
