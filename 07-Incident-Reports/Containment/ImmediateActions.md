# Immediate Containment Actions

## Overview

Following the detection of suspicious SMB authentication activity and PsExec-based remote execution, immediate containment actions were initiated to prevent further lateral movement and limit the impact of the simulated attack.

These actions were performed within the SOC Home Lab after confirming the malicious activity through Splunk Enterprise and Sysmon telemetry.

---

# Incident Summary

| Field | Value |
|-------|-------|
| Incident Type | Unauthorized Remote Administration Simulation |
| Severity | High |
| Detection Source | Splunk Enterprise |
| Primary Host | Windows-SOC |
| Attacker Host | Kali-SOC |
| Detection Phase | Phase 8 |

---

# Initial Assessment

The investigation identified:

- Successful SMB authentication
- Administrative share access
- PsExec service creation
- Remote command execution
- Discovery commands executed on the endpoint

Although the activity occurred within an isolated lab environment, it accurately simulated attacker behavior observed during real-world lateral movement incidents.

---

# Immediate Actions Taken

## 1. Confirm Detection

The SOC analyst verified:

- Splunk alerts
- Sysmon process creation events
- Windows Security logs
- SMB authentication records

Result:

> Malicious activity confirmed.

---

## 2. Identify Affected Systems

Affected systems included:

| System | Role |
|---------|------|
| Windows-SOC | Target Endpoint |
| Kali-SOC | Simulated Attacker |
| Ubuntu-SOC | Splunk Enterprise |

---

## 3. Preserve Evidence

Before making changes to the endpoint:

- Security logs were preserved.
- Sysmon events were collected.
- Splunk search results were exported.
- Screenshots were captured.
- Timeline reconstruction was initiated.

---

## 4. Stop Further Attacker Activity

To prevent additional simulated attacks:

- Remote administration activities were halted.
- Attack simulation was terminated.
- No additional commands were executed.

---

## 5. Notify Incident Response Team

Within a production environment this incident would be escalated to:

- SOC Team
- Incident Response Team
- System Administrators
- Management

Within this project, the incident response process was completed by the project author.

---

# Evidence Collected

Evidence preserved included:

- Process creation events
- SMB authentication logs
- Service installation events
- Registry activity
- Splunk dashboards
- Detection query results

---

# MITRE ATT&CK

| Tactic | Technique |
|---------|-----------|
| Lateral Movement | T1021.002 – SMB/Windows Admin Shares |
| Execution | T1569.002 – Service Execution |
| Discovery | T1082 – System Information Discovery |

---

# Outcome

Immediate containment successfully prevented any additional attack activity while preserving the forensic evidence required for threat hunting, incident reporting, and post-incident analysis. The environment was stabilized and prepared for eradication and recovery activities documented in the following sections.