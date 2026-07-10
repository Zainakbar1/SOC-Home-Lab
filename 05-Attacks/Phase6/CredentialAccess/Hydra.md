# Password Spraying Using Hydra

## Overview

Hydra was used to simulate a password spraying attack against the SMB service running on the Windows endpoint. The objective was to demonstrate how an attacker may attempt to validate credentials by trying a limited set of passwords across one or more user accounts.

This activity was performed in a controlled lab environment using authorized test accounts created specifically for the SOC Home Lab.

---

# Objective

- Simulate credential access techniques
- Validate SMB authentication
- Generate authentication telemetry
- Produce security events for Splunk detections
- Support threat hunting and incident response

---

# Environment

| Component | Value |
|-----------|-------|
| Attacker | Kali-SOC |
| Target | Windows-SOC |
| Attacker IP | 10.10.10.20 |
| Target IP | 10.10.10.30 |
| Tool | Hydra |
| Protocol | SMB |

---

# MITRE ATT&CK

| Tactic | Technique |
|--------|-----------|
| Credential Access | T1110.003 – Password Spraying |

---

# Tool Used

Hydra is an open-source password auditing tool capable of testing authentication against multiple network services.

Within this project, Hydra was used exclusively against the SMB service in the isolated SOC Home Lab.

---

# Commands Executed

## Password Spray

```bash
hydra -l socadmin -P passwords.txt smb://10.10.10.30
```

Example using multiple usernames:

```bash
hydra -L users.txt -P passwords.txt smb://10.10.10.30
```

---

# Expected Result

The attack should:

- Generate SMB authentication attempts
- Produce Windows Security Log events
- Generate network connections
- Create telemetry for Splunk detection

---

# Actual Result

Hydra successfully generated multiple SMB authentication attempts against the Windows endpoint. Authentication telemetry was collected through Windows Security Logs and Sysmon, then forwarded to Splunk Enterprise using the Splunk Universal Forwarder.

The generated events were later used to validate custom SPL detection rules and correlation searches.

---

# Detection Opportunities

Password spraying activity can generate:

- Multiple failed logons
- Repeated SMB authentication attempts
- Authentication from a single source host
- Rapid login attempts

Relevant Windows Event IDs include:

| Event ID | Description |
|----------|-------------|
| 4625 | Failed Logon |
| 4624 | Successful Logon |
| 4776 | NTLM Authentication |

Sysmon may also record:

| Event ID | Description |
|----------|-------------|
| 3 | Network Connection |

---

# Splunk Detection Opportunities

Possible detections include:

- Excessive failed logons
- Password spraying patterns
- SMB authentication anomalies
- Multiple authentication failures from one source
- Brute-force detection correlation searches

---

# Evidence

Related screenshots:

- Phase7-05 – Password Wordlist
- Phase7-06 – Hydra SMB Attempt
- Phase7-04 – Successful SMB Authentication

---

# Defensive Considerations

To reduce the effectiveness of password spraying attacks:

- Enforce strong password policies
- Implement account lockout thresholds
- Enable multi-factor authentication
- Monitor repeated authentication failures
- Alert on authentication attempts across multiple accounts
- Restrict SMB access where possible

---

# Follow-up Activities

Successful credential validation enabled:

- SMB Enumeration
- Share Enumeration
- PsExec Remote Execution
- Threat Hunting
- Incident Response

---

# Outcome

The Hydra password spraying simulation successfully generated authentication telemetry suitable for detection engineering. The resulting Windows Security events and Sysmon telemetry were ingested into Splunk Enterprise, where custom SPL queries and correlation searches were used to identify the attack and validate SOC monitoring capabilities.