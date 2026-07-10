# Evidence Collection Report

## Incident ID

IR-009

---

# Overview

This document catalogs all evidence collected during the Phase 8 investigation. The evidence was gathered from endpoint telemetry, Windows system artifacts, Sysmon logs, Splunk Enterprise, and analyst observations.

The objective is to preserve a complete record of investigative artifacts supporting the conclusions documented in the incident report.

---

# Evidence Summary

| Category | Items Collected |
|----------|----------------:|
| Endpoint Evidence | 8 |
| Registry Evidence | 2 |
| Scheduled Task Evidence | 1 |
| Process Evidence | 9 |
| Splunk Searches | 7 |
| Detection Rules | 7 |
| Correlation Searches | 3 |
| Alerts | 2 |
| Screenshots | 32 |

---

# Endpoint Evidence

## System Information

Host

```
windows-soc
```

User

```
socadmin
```

Operating System

```
Windows 11
```

Evidence Source

- hostname
- whoami
- systeminfo

---

## Running Processes

Evidence collected using:

```cmd
tasklist
```

Purpose

Identify running processes and confirm execution of attacker commands.

Evidence Status

✅ Collected

---

## Running Services

Evidence collected using:

```cmd
sc query
```

Purpose

Verify active Windows services and identify unauthorized services.

Evidence Status

✅ Collected

---

## Logged-On Users

Evidence collected using:

```cmd
quser
```

Purpose

Identify active interactive sessions.

Evidence Status

✅ Collected

---

## SMB Sessions

Evidence collected using:

```cmd
net session
```

Purpose

Identify active SMB connections that may indicate lateral movement.

Result

No active SMB sessions were identified.

Evidence Status

✅ Collected

---

# Registry Evidence

## Registry Path

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Purpose

Inspect Registry Run Keys for persistence.

---

## Registry Value

```text
ChromeUpdater
```

Associated Payload

```text
payload.bat
```

Evidence Source

```cmd
reg query
```

Evidence Status

✅ Collected

---

# Scheduled Task Evidence

Task Name

```text
ChromeUpdate
```

Trigger

```text
ONLOGON
```

Evidence Source

```cmd
schtasks /query
```

Evidence Status

✅ Collected

---

# Payload Evidence

File

```text
payload.bat
```

Location

```text
C:\Users\socadmin\Documents\
```

Purpose

Simulated persistence payload used for detection validation.

Evidence Status

✅ Collected

---

# Process Evidence

The following processes were observed and validated:

| Process | Purpose |
|----------|---------|
| whoami.exe | User Discovery |
| hostname.exe | Host Discovery |
| systeminfo.exe | System Discovery |
| ipconfig.exe | Network Discovery |
| net.exe | Account Discovery |
| tasklist.exe | Process Discovery |
| sc.exe | Service Discovery |
| reg.exe | Registry Activity |
| schtasks.exe | Scheduled Task Activity |

Evidence Source

- Sysmon Event ID 1
- Splunk Enterprise

---

# Splunk Evidence

The following searches were executed during the investigation:

| Search | Status |
|---------|--------|
| Discovery.spl | ✅ |
| RegistryPersistence.spl | ✅ |
| SchedulerTasks.spl | ✅ |
| IOC-Hunt.spl | ✅ |
| AttackTimeline.spl | ✅ |
| MITRE-Persistence.spl | ✅ |
| DetectionSummary.spl | ✅ |

---

# Detection Engineering Evidence

Validated Detection Rules

- Discovery Detection
- Registry Persistence Detection
- Scheduled Task Detection
- IOC Hunt
- Attack Timeline
- MITRE ATT&CK Persistence
- Detection Summary

Validation Status

✅ Successful

---

# Correlation Search Evidence

Validated Searches

- Discovery Detection
- Persistence Detection
- Threat Hunt

Validation Status

✅ Successful

---

# Alert Validation

The following alerts were successfully validated:

- Registry Persistence Alert
- Scheduled Task Persistence Alert

Both alerts generated expected results during attack simulation.

---

# MITRE ATT&CK Evidence

| ATT&CK ID | Technique |
|------------|-----------|
| T1033 | System Owner/User Discovery |
| T1082 | System Information Discovery |
| T1016 | Network Configuration Discovery |
| T1087 | Account Discovery |
| T1069 | Permission Group Discovery |
| T1057 | Process Discovery |
| T1007 | System Service Discovery |
| T1012 | Query Registry |
| T1547.001 | Registry Run Keys |
| T1053.005 | Scheduled Task |
| T1569.002 | Remote Service Execution |

---

# Screenshot Evidence

| Screenshot | Description |
|------------|-------------|
| 01–06 | Initial Assessment & Evidence Collection |
| 07–12 | Persistence Verification |
| 13–19 | Splunk Investigation |
| 20–22 | Discovery Activity |
| 23 | Registry Investigation |
| 24 | Registry Persistence |
| 25 | Payload Creation |
| 26 | Scheduled Task Creation |
| 27–28 | Remote Execution |
| 29 | IOC Hunt |
| 30 | Timeline Reconstruction |
| 31 | MITRE ATT&CK Mapping |
| 32 | Detection Summary |

---

# Evidence Integrity

The following practices were followed during evidence collection:

- Evidence gathered from original data sources
- Timeline reconstructed from centralized logs
- Commands documented during execution
- Screenshots captured during each investigation phase
- Findings validated using multiple data sources
- No evidence modified after collection

---

# Evidence Assessment

The collected evidence was sufficient to:

- Reconstruct the attack timeline
- Identify persistence mechanisms
- Validate detection rules
- Confirm IOC presence
- Map attacker behavior to MITRE ATT&CK
- Support incident response conclusions

All evidence was consistent with the controlled attack simulation performed during Phase 8.

---

# Conclusion

Evidence collected throughout the investigation confirmed successful execution and detection of the simulated attack. Endpoint telemetry, Splunk searches, Registry artifacts, Scheduled Tasks, and IOC analysis collectively provided a complete forensic record of attacker activity.

The evidence supported all findings documented in **IR-009** and demonstrated the effectiveness of the implemented detection engineering and threat hunting workflows.