# Incident Report IR-007

## PsExec Remote Execution Investigation

---

# Incident Information

| Field | Value |
|--------|-------|
| Incident ID | IR-007 |
| Severity | High |
| Status | Closed |
| Analyst | Akbar Md |

---

# Executive Summary

A simulated remote execution scenario was performed using Impacket PsExec from the Kali attack workstation against the Windows endpoint.

The objective was to validate endpoint telemetry generation and verify detection engineering rules for remote command execution.

---

# Systems

Source

- Kali-SOC

Target

- Windows-SOC

---

# Activity Observed

Remote execution of:

- whoami
- hostname
- systeminfo
- ipconfig
- tasklist
- reg query
- schtasks /query

---

# Evidence

Telemetry collected from:

- Sysmon Event ID 1
- Splunk Enterprise
- Process Creation Logs

---

# Detection

Validated Queries

- Discovery.spl
- IOC-Hunt.spl
- AttackTimeline.spl

---

# MITRE ATT&CK

| Technique | ID |
|------------|----|
| Remote Service Execution | T1569.002 |
| System Discovery | T1082 |
| Account Discovery | T1087 |

---

# Findings

Observed:

- Remote process creation
- Discovery commands
- Registry access
- Scheduled task enumeration

No persistence remained after cleanup.

---

# Conclusion

Remote execution telemetry was successfully collected and analyzed. Detection rules accurately identified attacker activity, supporting threat hunting and timeline reconstruction.