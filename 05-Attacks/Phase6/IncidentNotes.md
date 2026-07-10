# Phase 6 Incident Notes

## Overview

Phase 6 focused on simulating a realistic attacker workflow against the Windows endpoint within the SOC Home Lab. The objective was to generate security telemetry that could later be analyzed using Splunk Enterprise, validate custom detection rules, and support threat hunting and incident response activities.

All activities were performed within an isolated VMware-based lab using authorized systems owned by the project.

---

# Phase Objective

The objectives of this phase were to:

- Perform reconnaissance against the Windows endpoint
- Enumerate available services
- Validate SMB accessibility
- Simulate credential access
- Prepare for remote execution
- Generate endpoint telemetry
- Validate detection engineering workflows

---

# Environment

| Component | Value |
|----------|-------|
| Attacker | Kali-SOC |
| Target | Windows-SOC |
| SIEM | Splunk Enterprise |
| Endpoint Monitoring | Sysmon |
| Log Forwarder | Splunk Universal Forwarder |

---

# Attack Timeline

| Step | Activity |
|------|----------|
| 1 | Host Discovery |
| 2 | Port Scanning |
| 3 | Service Enumeration |
| 4 | SMB Enumeration |
| 5 | Password Spraying |
| 6 | Credential Validation |
| 7 | Preparation for PsExec Execution |

---

# Attack Chain

```
Host Discovery
        │
        ▼
Port Scan
        │
        ▼
Service Enumeration
        │
        ▼
SMB Enumeration
        │
        ▼
Password Spraying
        │
        ▼
Credential Validation
        │
        ▼
Remote Execution (Phase 7)
```

---

# Tools Used

- Nmap
- NetExec
- Hydra
- smbclient
- Kali Linux
- Sysmon
- Splunk Enterprise

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Discovery | Network Service Discovery | T1046 |
| Discovery | Network Share Discovery | T1135 |
| Credential Access | Password Spraying | T1110.003 |
| Lateral Movement | SMB / Windows Admin Shares | T1021.002 |

---

# Evidence Collected

The following evidence was generated during this phase:

- ICMP connectivity
- TCP connection attempts
- Open port identification
- SMB authentication events
- SMB share enumeration
- Windows Security Events
- Sysmon Network Events
- Splunk search results

---

# Detection Validation

The telemetry generated during this phase was successfully detected using:

- SPL Queries
- Correlation Searches
- Alert Rules
- IOC Hunting
- Timeline Reconstruction

---

# Lessons Learned

Key observations from this phase include:

- Reconnaissance activities generate valuable telemetry even before exploitation.
- SMB authentication events provide strong indicators for monitoring lateral movement.
- Sysmon significantly improves endpoint visibility compared to native Windows logs alone.
- Correlating multiple low-level events provides better detection coverage than relying on single-event alerts.

---

# Phase Outcome

Phase 6 successfully established the initial stages of the simulated attack lifecycle. Reconnaissance, service enumeration, SMB enumeration, and credential access activities generated realistic telemetry that served as the foundation for:

- Phase 7 – Lateral Movement and PsExec Execution
- Phase 8 – Threat Hunting and Incident Response
- Detection Engineering
- MITRE ATT&CK Mapping
- Final Incident Reporting

The objectives of Phase 6 were successfully completed and validated through Splunk searches, Sysmon events, and documented evidence.