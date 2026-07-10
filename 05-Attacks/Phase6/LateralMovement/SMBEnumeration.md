# SMB Enumeration

## Overview

SMB Enumeration was performed after identifying the SMB service on the Windows endpoint. The objective was to enumerate accessible SMB shares, verify authentication, and determine whether remote administration was possible.

This activity represents a common attacker technique used to identify shared resources, gather information, and prepare for lateral movement within a Windows environment.

---

# Objective

- Verify SMB connectivity
- Enumerate available SMB shares
- Test authentication
- Identify accessible resources
- Prepare for remote execution
- Generate telemetry for detection validation

---

# Environment

| Component | Value |
|-----------|-------|
| Attacker | Kali-SOC |
| Target | Windows-SOC |
| Attacker IP | 10.10.10.20 |
| Target IP | 10.10.10.30 |
| Protocol | SMB |
| Port | TCP 445 |

---

# MITRE ATT&CK

| Tactic | Technique |
|--------|-----------|
| Discovery | T1135 – Network Share Discovery |
| Lateral Movement | T1021.002 – SMB/Windows Admin Shares |

---

# Tools Used

- NetExec (formerly CrackMapExec)
- smbclient
- Nmap SMB NSE Scripts

---

# Commands Executed

## Verify SMB Service

```bash
nmap -Pn -p445 10.10.10.30
```

---

## Authenticate Using NetExec

```bash
netexec smb 10.10.10.30 -u socadmin -p <password>
```

---

## Enumerate SMB Shares

```bash
netexec smb 10.10.10.30 -u socadmin -p <password> --shares
```

---

## Enumerate Shares Using smbclient

```bash
smbclient -L //10.10.10.30 -U socadmin
```

---

## Verify SMB Protocol

```bash
nmap --script smb-protocols -p445 10.10.10.30
```

---

# Expected Result

Successful authentication should allow:

- Enumeration of shared folders
- Identification of administrative shares
- Verification of remote access capability
- Preparation for PsExec execution

---

# Actual Result

Authentication to the Windows endpoint was successful using valid credentials. SMB shares were enumerated, confirming that administrative access was available. The collected information validated that the environment supported remote administration and allowed progression to PsExec-based remote execution.

---

# Detection Opportunities

SMB enumeration may generate telemetry including:

- Successful SMB authentication
- Network logon events
- SMB session establishment
- Share enumeration activity
- Administrative share access

Relevant Windows Event IDs include:

| Event ID | Description |
|----------|-------------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 5140 | Network Share Access |
| 5145 | Detailed File Share Access |

Sysmon may also record:

- Event ID 3 – Network Connection

---

# Splunk Detection Opportunities

The following detections can identify SMB enumeration:

- Successful SMB authentication
- Administrative share access
- Multiple SMB connections from a single host
- Authentication followed by share enumeration
- Suspicious lateral movement activity

---

# Evidence

Related screenshots:

- Phase7-03 – SMB Port Verification
- Phase7-04 – NetExec Successful Authentication
- Phase7-07 – NetExec Share Enumeration
- Phase7-10 – smbclient Share Enumeration
- Phase7-11 – NetExec Share Enumeration

---

# Follow-up Activities

Successful SMB enumeration enabled:

- Credential Validation
- PsExec Remote Execution
- Threat Hunting
- Detection Engineering
- Incident Response Analysis

---

# Defensive Considerations

Organizations can reduce the risk of SMB-based attacks by:

- Restricting SMB exposure
- Disabling unnecessary administrative shares
- Enforcing strong authentication
- Monitoring Event IDs 4624, 5140, and 5145
- Detecting unusual SMB authentication patterns
- Alerting on administrative share enumeration

---

# Outcome

SMB Enumeration successfully identified accessible network shares and verified administrative access to the Windows endpoint. The information gathered during this phase directly supported the PsExec remote execution simulation and provided valuable telemetry for Splunk detection engineering and threat hunting.