# Incident Timeline

## Incident ID

IR-009

---

# Overview

This document reconstructs the sequence of events observed during the Phase 8 investigation. The timeline was created using Sysmon telemetry, Windows event logs, and Splunk Enterprise searches to establish a chronological view of attacker activity.

The objective is to determine the progression of the simulated attack, identify persistence mechanisms, and correlate all observed evidence into a single investigative timeline.

---

# Investigation Summary

| Incident ID | IR-009 |
|--------------|---------|
| Incident Type | Threat Hunting |
| Severity | High |
| Status | Closed |
| Analyst | Akbar Md |

---

# Timeline

## Stage 1 – Initial Discovery

### Activity

The investigation identified execution of multiple Windows discovery commands.

### Commands Observed

```cmd
whoami
hostname
systeminfo
ipconfig /all
```

### Purpose

Collect information about the compromised endpoint.

### Evidence

- Sysmon Event ID 1
- Process Creation
- Command Line Logging

### Screenshots

20

---

## Stage 2 – Account Enumeration

### Activity

Enumeration of local users and privileged groups.

### Commands

```cmd
net user

net localgroup administrators

net localgroup "Remote Desktop Users"
```

### Purpose

Identify available accounts and administrative privileges.

### Evidence

Process Creation Events

### Screenshots

21

---

## Stage 3 – System Enumeration

### Activity

Enumeration of processes, services, and scheduled tasks.

### Commands

```cmd
tasklist

sc query

schtasks /query
```

### Purpose

Understand running services and identify existing persistence mechanisms.

### Screenshots

22

---

## Stage 4 – Registry Investigation

### Activity

Registry Run Keys examined.

### Commands

```cmd
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run

reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
```

### Purpose

Search for existing persistence.

### Evidence

Sysmon Process Creation

### Screenshots

23

---

## Stage 5 – Registry Persistence

### Activity

Creation of Registry Run Key.

### Registry

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

### Value

```text
ChromeUpdater
```

### Payload

```text
payload.bat
```

### MITRE ATT&CK

T1547.001

### Evidence

- reg.exe
- Registry Modification
- Sysmon Process Creation

### Screenshots

24

---

## Stage 6 – Payload Deployment

### Activity

A demonstration batch file was created to simulate a payload referenced by persistence mechanisms.

### File

```text
payload.bat
```

### Location

```text
C:\Users\socadmin\Documents\
```

### Evidence

Screenshot

25

---

## Stage 7 – Scheduled Task Persistence

### Activity

A Scheduled Task named **ChromeUpdate** was created.

### Trigger

```text
ONLOGON
```

### Payload

```text
payload.bat
```

### MITRE ATT&CK

T1053.005

### Evidence

- schtasks.exe
- Process Creation
- Command Line Logging

### Screenshots

26

---

## Stage 8 – Remote Execution

### Activity

Remote commands executed using Impacket PsExec.

### Commands

```cmd
hostname

whoami

systeminfo

ipconfig

tasklist

reg query

schtasks /query
```

### Purpose

Simulate lateral movement and post-compromise administration.

### Evidence

- Sysmon Event ID 1
- Parent Process
- SYSTEM Context
- Command Line

### Screenshots

27

28

---

## Stage 9 – IOC Hunting

### Activity

Indicators of Compromise identified.

### Indicators

- payload.bat
- ChromeUpdater
- ChromeUpdate

### Evidence

Splunk IOC Hunt

### Screenshot

29

---

## Stage 10 – Timeline Reconstruction

### Activity

All collected telemetry was sorted chronologically to reconstruct attacker behavior.

### Data Used

- Timestamp
- User
- Parent Process
- Process Name
- Command Line

### Screenshot

30

---

## Stage 11 – MITRE ATT&CK Correlation

### Activity

Observed techniques mapped to MITRE ATT&CK.

### Techniques Identified

- T1033
- T1082
- T1016
- T1087
- T1069
- T1057
- T1007
- T1012
- T1547.001
- T1053.005
- T1569.002

### Screenshot

31

---

## Stage 12 – Detection Validation

### Activity

Detection engineering rules validated using generated telemetry.

### Validated Detections

- Discovery Detection
- Registry Persistence
- Scheduled Task Detection
- IOC Hunt
- Attack Timeline
- MITRE Mapping

### Screenshot

32

---

# Timeline Summary

```
Discovery
      │
      ▼
Account Enumeration
      │
      ▼
System Enumeration
      │
      ▼
Registry Investigation
      │
      ▼
Registry Persistence
      │
      ▼
Payload Deployment
      │
      ▼
Scheduled Task Persistence
      │
      ▼
Remote Execution
      │
      ▼
IOC Hunting
      │
      ▼
Timeline Reconstruction
      │
      ▼
MITRE ATT&CK Correlation
      │
      ▼
Detection Validation
```

---

# Analyst Assessment

The chronological reconstruction confirmed that the simulated attack followed a structured sequence beginning with discovery and ending with persistence establishment and validation.

Each stage generated endpoint telemetry that was successfully collected by Sysmon and analyzed within Splunk Enterprise. The timeline provided investigators with a clear understanding of attacker behavior, enabling rapid identification of persistence mechanisms, Indicators of Compromise, and associated MITRE ATT&CK techniques.

No unexpected or unauthorized activity was identified beyond the planned simulation.

---

# Evidence References

| Screenshot | Description |
|------------|-------------|
| 20 | Discovery Activity |
| 21 | Account Enumeration |
| 22 | System Enumeration |
| 23 | Registry Investigation |
| 24 | Registry Persistence |
| 25 | Payload Creation |
| 26 | Scheduled Task Creation |
| 27 | Remote Execution |
| 28 | Remote Telemetry |
| 29 | IOC Hunt |
| 30 | Timeline Reconstruction |
| 31 | MITRE ATT&CK Mapping |
| 32 | Detection Validation |

---

# Conclusion

The incident timeline successfully reconstructed the complete attack sequence performed during Phase 8. By correlating Sysmon telemetry with Splunk searches, the investigation established a clear chronology of discovery, persistence, remote execution, IOC generation, and detection validation. This timeline served as the foundation for evidence analysis, containment verification, and final incident reporting.