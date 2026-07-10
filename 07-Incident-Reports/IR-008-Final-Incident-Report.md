# Incident Report IR-008

## Final Incident Response Summary

---

# Executive Summary

This report summarizes the complete attack simulation conducted within the SOC Home Lab, covering attack execution, detection engineering, threat hunting, and incident response.

The objective was to validate the effectiveness of the deployed SOC infrastructure and demonstrate practical blue-team capabilities.

---

# Attack Stages

1. Discovery
2. Enumeration
3. Registry Investigation
4. Registry Persistence
5. Scheduled Task Persistence
6. Remote Execution
7. IOC Hunting
8. Timeline Reconstruction

---

# Detection Summary

Successfully Validated:

- Discovery Detection
- Registry Persistence
- Scheduled Task Detection
- IOC Hunt
- Attack Timeline
- MITRE Mapping

---

# Indicators of Compromise

Files

- payload.bat

Registry

- ChromeUpdater

Scheduled Task

- ChromeUpdate

---

# MITRE ATT&CK Coverage

- T1033
- T1082
- T1016
- T1087
- T1057
- T1007
- T1012
- T1547.001
- T1053.005
- T1569.002

---

# Evidence

Collected:

- Sysmon Logs
- Splunk Searches
- Screenshots
- Timeline
- Registry Artifacts
- Scheduled Tasks

---

# Lessons Learned

- Endpoint telemetry is critical for visibility.
- Detection engineering requires tuning.
- Timeline reconstruction improves investigations.
- MITRE ATT&CK provides standardized documentation.
- Threat hunting complements alert-driven monitoring.

---

# Final Assessment

The SOC Home Lab successfully demonstrated an end-to-end incident response workflow from attack simulation through detection, investigation, containment validation, and reporting.

The project validates practical skills in:

- SOC Operations
- Detection Engineering
- Threat Hunting
- Incident Response
- Splunk Enterprise
- Sysmon
- MITRE ATT&CK
- Windows Endpoint Investigation

---

# Status

**Closed**

All simulated persistence mechanisms were removed, detections validated, and the environment returned to a known-good state.