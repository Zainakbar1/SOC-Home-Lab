# IOC Analysis Report

## Incident ID

IR-009

---

# Overview

This document contains a detailed analysis of all Indicators of Compromise (IOCs) identified during the Phase 8 threat hunting investigation.

The purpose of IOC analysis is to identify malicious artifacts, determine their origin, understand their impact, and assist in containment, eradication, and future detection engineering.

All IOCs listed in this report were intentionally generated within the SOC Home Lab for defensive training and validation purposes.

---

# IOC Summary

| IOC Type | Count |
|-----------|------:|
| Files | 1 |
| Registry Values | 1 |
| Scheduled Tasks | 1 |
| Processes | 9 |
| Registry Paths | 1 |
| Commands | Multiple |

---

# File Indicators

## IOC 1

### File Name

```text
payload.bat
```

### Location

```text
C:\Users\socadmin\Documents\
```

### Purpose

The batch file was created to simulate a payload referenced by Registry Run Key persistence and Scheduled Task persistence.

### Risk

Low

The payload contains only demonstration commands and performs no malicious activity.

### Detection

Detected by:

- Sysmon
- Splunk Enterprise

Evidence

Screenshot 25

---

# Registry Indicators

## Registry Path

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

---

## Registry Value

```text
ChromeUpdater
```

---

## Associated Payload

```text
payload.bat
```

---

## MITRE ATT&CK

T1547.001

Registry Run Keys / Startup Folder

---

## Detection

Detected through:

```spl
Image="*reg.exe"

CurrentVersion\Run

ChromeUpdater
```

Evidence

Screenshots

23

24

---

# Scheduled Task Indicators

## Task Name

```text
ChromeUpdate
```

---

## Trigger

```text
ONLOGON
```

---

## Payload

```text
payload.bat
```

---

## MITRE ATT&CK

T1053.005

Scheduled Task / Job

---

## Detection

Detected using:

```spl
Image="*schtasks.exe"

CommandLine="*ChromeUpdate*"
```

Evidence

Screenshots

25

26

---

# Process Indicators

The following processes were observed during the investigation.

| Process | Purpose |
|----------|----------|
| whoami.exe | User Discovery |
| hostname.exe | Host Discovery |
| systeminfo.exe | System Discovery |
| ipconfig.exe | Network Discovery |
| net.exe | Account Discovery |
| tasklist.exe | Process Discovery |
| sc.exe | Service Discovery |
| reg.exe | Registry Activity |
| schtasks.exe | Scheduled Task Activity |

---

# Registry Activity

Observed Registry Operations

```text
Query Registry

Create Registry Run Key

Validate Registry Run Key
```

Detection

- RegistryPersistence.spl
- IOC-Hunt.spl

---

# Persistence Indicators

Persistence techniques observed:

## Registry Run Key

```
ChromeUpdater
```

---

## Scheduled Task

```
ChromeUpdate
```

---

## Associated Payload

```
payload.bat
```

---

# Command Line Indicators

The following command-line activity was identified:

```cmd
reg query

reg add

schtasks /create

whoami

hostname

systeminfo

tasklist

ipconfig

net user

sc query
```

These commands were successfully captured by Sysmon Event ID 1 and ingested into Splunk Enterprise.

---

# MITRE ATT&CK Mapping

| IOC | Technique | ATT&CK ID |
|------|-----------|-----------|
| whoami.exe | System Owner/User Discovery | T1033 |
| hostname.exe | System Information Discovery | T1082 |
| ipconfig.exe | Network Configuration Discovery | T1016 |
| net.exe | Account Discovery | T1087 |
| tasklist.exe | Process Discovery | T1057 |
| sc.exe | Service Discovery | T1007 |
| reg.exe | Query Registry | T1012 |
| ChromeUpdater | Registry Run Keys | T1547.001 |
| ChromeUpdate | Scheduled Task | T1053.005 |

---

# IOC Investigation

Each IOC was investigated to determine:

- Origin
- Purpose
- Execution context
- Parent process
- Associated user
- Detection status
- Related persistence
- Timeline position

All indicators correlated with the simulated attacker activity executed during Phase 8.

---

# Containment Status

| IOC | Status |
|------|--------|
| payload.bat | Removed |
| ChromeUpdater | Removed |
| ChromeUpdate | Removed |

No persistence remained after remediation.

---

# Detection Status

| IOC | Detection |
|------|-----------|
| payload.bat | ✅ |
| ChromeUpdater | ✅ |
| ChromeUpdate | ✅ |
| reg.exe | ✅ |
| schtasks.exe | ✅ |
| Discovery Commands | ✅ |

---

# Analyst Notes

No unknown or unexpected indicators were identified during the investigation.

All observed IOCs were directly attributable to the controlled attack simulation performed within the SOC Home Lab.

The investigation successfully demonstrated the complete lifecycle of IOC identification, validation, correlation, and removal.

---

# Evidence

Screenshots referenced:

- 23 – Registry Discovery
- 24 – Registry Persistence
- 25 – Payload Creation
- 26 – Scheduled Task Creation
- 29 – IOC Hunt
- 32 – Detection Summary

---

# Conclusion

The IOC analysis confirmed successful detection of all simulated attacker artifacts generated during Phase 8. Registry persistence, scheduled task persistence, discovery commands, and payload references were identified using Sysmon telemetry and Splunk Enterprise searches. Following validation, all persistence mechanisms and associated artifacts were removed, leaving the endpoint in a verified clean state.