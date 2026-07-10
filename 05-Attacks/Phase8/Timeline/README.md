# Attack Timeline

## Overview

This document reconstructs the complete attack sequence executed during Phase 8. The timeline is based on endpoint telemetry collected by Sysmon, centralized in Splunk Enterprise, and correlated using Splunk Search Processing Language (SPL).

Each activity is mapped to the corresponding MITRE ATT&CK technique and includes the expected telemetry generated during execution.

---

# Attack Summary

| Attacker | Kali-SOC |
|----------|----------|
| Source IP | 10.10.10.20 |
| Target | Windows-SOC |
| Target IP | 10.10.10.30 |
| SIEM | Ubuntu-SOC (Splunk Enterprise) |

---

# Timeline

## Stage 1 – Initial Discovery

### Commands

```cmd
whoami
hostname
systeminfo
ipconfig /all
```

### Purpose

Gather basic information about the compromised endpoint.

### MITRE ATT&CK

| Technique | ID |
|-----------|----|
| System Owner/User Discovery | T1033 |
| System Information Discovery | T1082 |
| Network Configuration Discovery | T1016 |

### Telemetry

- Sysmon Event ID 1
- Process Creation
- Parent Process
- Command Line

### Evidence

Screenshot 20

---

# Stage 2 – Account Enumeration

### Commands

```cmd
net user

net localgroup administrators

net localgroup "Remote Desktop Users"
```

### Purpose

Identify local users and privileged accounts.

### MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Account Discovery | T1087 |
| Permission Group Discovery | T1069 |

### Evidence

Screenshot 21

---

# Stage 3 – Process and Service Discovery

### Commands

```cmd
tasklist

sc query

schtasks /query
```

### Purpose

Enumerate active processes, Windows services, and scheduled tasks.

### MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Process Discovery | T1057 |
| Service Discovery | T1007 |
| Scheduled Task Discovery | T1053.005 |

### Evidence

Screenshot 22

---

# Stage 4 – Registry Discovery

### Commands

```cmd
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run

reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

### Purpose

Search for existing persistence mechanisms.

### MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Query Registry | T1012 |

### Evidence

Screenshot 23

---

# Stage 5 – Registry Persistence

### Command

```cmd
reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Run ^
/v ChromeUpdater ^
/t REG_SZ ^
/d "C:\Users\socadmin\Documents\payload.bat" ^
/f
```

### Purpose

Create a Registry Run Key to simulate persistence.

### MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Registry Run Keys / Startup Folder | T1547.001 |

### Generated IOC

| IOC | Type |
|------|------|
| ChromeUpdater | Registry Value |

### Evidence

Screenshot 24

---

# Stage 6 – Payload Deployment

### Payload

```bat
@echo off
echo Fake Payload Executed
pause
```

### File

```
payload.bat
```

### Location

```
C:\Users\socadmin\Documents\
```

### Purpose

Simulate an attacker-deployed payload without performing malicious actions.

### Evidence

Screenshot 25

---

# Stage 7 – Scheduled Task Persistence

### Command

```cmd
schtasks /create ^
/tn ChromeUpdate ^
/tr "C:\Users\socadmin\Documents\payload.bat" ^
/sc ONLOGON ^
/ru SYSTEM
```

### Purpose

Simulate persistence using a scheduled task.

### MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Scheduled Task/Job | T1053.005 |

### Generated IOC

| IOC | Type |
|------|------|
| ChromeUpdate | Scheduled Task |

### Evidence

Screenshot 26

---

# Stage 8 – Remote Execution

### Tool

Impacket PsExec

### Commands Executed

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

Simulate post-compromise remote administration.

### MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Remote Service Execution | T1569.002 |

### Generated Telemetry

- Process Creation
- Parent Process
- SYSTEM Context
- Command Line Logging

### Evidence

Screenshots

27

28

---

# Stage 9 – IOC Hunting

### Indicators Investigated

- payload.bat
- ChromeUpdater
- ChromeUpdate
- reg.exe
- schtasks.exe
- tasklist.exe
- systeminfo.exe

### Splunk Query

```spl
index=sysmon earliest=-30m
(
CommandLine="*ChromeUpdate*"
OR CommandLine="*payload.bat*"
OR CommandLine="*CurrentVersion\\Run*"
OR Image="*schtasks.exe"
OR Image="*reg.exe"
)
| table _time User Image ParentImage CommandLine
| sort -_time
```

### Evidence

Screenshot 29

---

# Stage 10 – Timeline Reconstruction

A chronological reconstruction of attacker activity was performed using Splunk.

### Fields Used

- Timestamp
- User
- Parent Process
- Process
- Command Line

### Evidence

Screenshot 30

---

# Stage 11 – MITRE ATT&CK Mapping

The simulated attack covered multiple ATT&CK tactics.

| Activity | ATT&CK ID |
|----------|-----------|
| User Discovery | T1033 |
| System Discovery | T1082 |
| Network Discovery | T1016 |
| Account Discovery | T1087 |
| Permission Group Discovery | T1069 |
| Process Discovery | T1057 |
| Service Discovery | T1007 |
| Registry Discovery | T1012 |
| Registry Persistence | T1547.001 |
| Scheduled Task Persistence | T1053.005 |
| Remote Service Execution | T1569.002 |

### Evidence

Screenshot 31

---

# Stage 12 – Detection Validation

Detection engineering rules successfully identified:

- Discovery commands
- Registry modifications
- Registry persistence
- Scheduled task creation
- IOC generation
- Timeline reconstruction

### Evidence

Screenshot 32

---

# Complete Attack Flow

```
Initial Access (Existing Administrative Access)
            │
            ▼
System Discovery
            │
            ▼
Account Enumeration
            │
            ▼
Process & Service Discovery
            │
            ▼
Registry Discovery
            │
            ▼
Registry Persistence
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
Detection Validation
```

---

# Timeline Outcome

The attack sequence successfully generated realistic endpoint telemetry covering discovery, persistence, remote execution, and attacker artifact creation. All activities were captured by Sysmon and analyzed using Splunk Enterprise, enabling complete reconstruction of the attack timeline and validation of detection engineering use cases within the SOC Home Lab.