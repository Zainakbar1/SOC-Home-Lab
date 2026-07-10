# Persistence Phase

## Overview

Following successful discovery, the attacker attempted to establish persistence on the compromised Windows endpoint. Persistence ensures that access can be regained after a reboot or user logon without requiring exploitation again.

In this phase, two common persistence techniques were safely simulated:

- Registry Run Key Persistence
- Scheduled Task Persistence

Both techniques generated endpoint telemetry that was successfully collected by Sysmon and forwarded to Splunk Enterprise for detection and investigation.

---

# Objectives

The objectives of this phase were to:

- Simulate Registry Run Key persistence
- Simulate Scheduled Task persistence
- Generate realistic endpoint telemetry
- Validate Sysmon logging
- Validate Splunk detections
- Produce Indicators of Compromise (IOCs)

---

# Target System

| Host | Windows-SOC |
|------|-------------|
| IP Address | 10.10.10.30 |
| User | socadmin |

---

# Persistence Technique 1 – Registry Run Key

## Description

Windows Registry Run Keys automatically execute specified programs whenever a user logs on. Attackers frequently abuse this mechanism to maintain persistence.

Registry Location:

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

---

## Command Executed

```cmd
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" ^
/v ChromeUpdater ^
/t REG_SZ ^
/d "C:\Users\socadmin\Documents\payload.bat" ^
/f
```

---

## Registry Value

| Name | Value |
|------|-------|
| ChromeUpdater | C:\Users\socadmin\Documents\payload.bat |

---

## Purpose

The Registry value was created to simulate an attacker configuring a payload to execute automatically when the user logs on.

No malicious executable was used. The payload consisted of a harmless batch file created solely for lab purposes.

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Registry Run Keys / Startup Folder | T1547.001 |

---

## Generated Telemetry

Sysmon captured:

- Process Creation (Event ID 1)
- reg.exe execution
- PowerShell parent process
- Command Line
- User Context

---

## Detection

Splunk Query

```spl
index=sysmon
Image="*reg.exe"
OR CommandLine="*ChromeUpdater*"
```

Detection Status

✅ Successfully Detected

---

# Persistence Technique 2 – Scheduled Task

## Description

Windows Scheduled Tasks allow programs to execute automatically based on predefined triggers. Adversaries frequently create scheduled tasks to maintain persistence after compromise.

---

## Task Information

| Task Name | ChromeUpdate |
|-----------|--------------|
| Trigger | ONLOGON |
| Payload | payload.bat |

---

## Command Executed

```cmd
schtasks /create ^
/tn ChromeUpdate ^
/tr "C:\Users\socadmin\Documents\payload.bat" ^
/sc ONLOGON ^
/ru SYSTEM
```

---

## Purpose

Simulate persistence through scheduled task creation while generating telemetry suitable for threat hunting and detection engineering.

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Scheduled Task/Job | T1053.005 |

---

## Generated Telemetry

Sysmon recorded:

- schtasks.exe
- CommandLine
- ParentImage
- User
- Process Creation

---

## Detection

Splunk Query

```spl
index=sysmon
Image="*schtasks.exe"
OR CommandLine="*ChromeUpdate*"
```

Detection Status

✅ Successfully Detected

---

# Payload

The following payload was used for persistence simulation:

```bat
@echo off
echo Fake Payload Executed
pause
```

Location

```text
C:\Users\socadmin\Documents\payload.bat
```

The payload performs no malicious activity and exists only to emulate attacker behavior.

---

# Indicators of Compromise (IOCs)

| IOC | Type |
|------|------|
| ChromeUpdater | Registry Value |
| ChromeUpdate | Scheduled Task |
| payload.bat | Batch File |
| reg.exe | Process |
| schtasks.exe | Process |

---

# Detection Opportunities

The following behaviors can be detected:

- Registry Run Key creation
- Registry modifications
- Scheduled Task creation
- Execution of reg.exe
- Execution of schtasks.exe
- PowerShell launching persistence commands

---

# Splunk Searches

Registry Persistence

```spl
index=sysmon
Image="*reg.exe"
```

Scheduled Task Persistence

```spl
index=sysmon
Image="*schtasks.exe"
```

IOC Hunt

```spl
index=sysmon
(CommandLine="*ChromeUpdater*"
OR CommandLine="*ChromeUpdate*"
OR CommandLine="*payload.bat*")
```

---

# Evidence

| Screenshot | Description |
|------------|-------------|
| 23 | Registry Discovery |
| 24 | Registry Persistence |
| 25 | Payload Creation |
| 26 | Scheduled Task Creation |

---

# Outcome

This phase successfully simulated two common Windows persistence mechanisms used by adversaries. Registry Run Keys and Scheduled Tasks were created in a controlled laboratory environment to generate realistic endpoint telemetry. Sysmon successfully captured the associated process creation events, and Splunk Enterprise was used to validate detections, identify indicators of compromise, and support subsequent threat hunting and incident response activities.