# System Isolation

## Overview

Following confirmation of unauthorized SMB authentication and PsExec-based remote execution, the affected Windows endpoint was logically isolated to prevent further attacker activity while preserving forensic evidence.

In a production Security Operations Center (SOC), isolation is one of the highest-priority containment actions because it limits lateral movement without immediately destroying valuable evidence.

Within this SOC Home Lab, the isolation process was simulated using administrative controls while maintaining the integrity of the investigation.

---

# Objective

The objectives of system isolation were to:

- Prevent additional attacker activity
- Stop lateral movement
- Preserve forensic evidence
- Maintain log integrity
- Protect unaffected systems
- Prepare the endpoint for eradication

---

# Affected System

| Component | Value |
|-----------|-------|
| Hostname | Windows-SOC |
| Operating System | Windows 11 |
| IP Address | 10.10.10.30 |
| Incident Type | SMB Lateral Movement / PsExec Execution |
| Severity | High |

---

# Isolation Strategy

The following containment strategy was adopted:

1. Confirm malicious activity.
2. Preserve volatile evidence.
3. Stop the active attack simulation.
4. Prevent additional remote access.
5. Maintain Splunk connectivity until evidence collection completed.
6. Prepare the endpoint for forensic review.

---

# Simulated Isolation Actions

The following actions were documented as part of the incident response exercise:

- Disable unnecessary remote administration.
- Restrict SMB access.
- Block attacker connectivity.
- Suspend additional attack execution.
- Preserve event logs.
- Continue telemetry collection until evidence acquisition was complete.

---

# Evidence Preserved

Prior to isolation, the following evidence was collected:

- Sysmon Operational Logs
- Windows Security Event Logs
- Process Creation Events
- Network Connection Events
- Registry Modification Events
- Splunk Search Results
- Timeline Reconstruction
- IOC Reports

---

# Verification

Isolation effectiveness was verified by confirming:

- No additional SMB sessions were established.
- No new PsExec service installations occurred.
- No new remote process creation events appeared.
- No further attacker commands were executed.

Splunk searches confirmed that malicious activity had ceased following containment.

---

# MITRE ATT&CK Mapping

| Tactic | Technique |
|---------|-----------|
| Lateral Movement | T1021.002 – SMB/Windows Admin Shares |
| Execution | T1569.002 – Service Execution |
| Discovery | T1082 – System Information Discovery |

---

# Lessons Learned

This exercise highlighted several important principles:

- Isolation should occur only after sufficient evidence has been collected.
- Premature shutdown of a compromised endpoint may destroy valuable forensic artifacts.
- Continuous monitoring through Splunk provides confidence that containment actions were successful.
- Well-documented isolation procedures reduce incident response time and improve investigation quality.

---

# Outcome

System isolation successfully contained the simulated attack while preserving the telemetry required for forensic analysis. The Windows endpoint was stabilized without affecting the integrity of the collected evidence, allowing the investigation to proceed to the eradication phase.