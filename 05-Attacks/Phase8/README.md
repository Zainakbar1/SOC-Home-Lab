# Phase 08 – Advanced Attack Simulation

## Overview

This phase extends the attack scenarios performed in Phases 6 and 7 by simulating a complete adversary workflow against the Windows endpoint. The objective is to generate realistic endpoint telemetry for detection engineering, threat hunting, and incident response exercises.

Unlike previous phases that focused on reconnaissance and initial lateral movement, this phase introduces attacker discovery, persistence mechanisms, registry modifications, scheduled tasks, and remote command execution.

All activities were executed in an isolated VMware lab and were designed solely for defensive research and SOC training.

---

# Objectives

The objectives of this phase were:

- Generate realistic Sysmon telemetry
- Simulate attacker discovery
- Simulate registry-based persistence
- Simulate scheduled task persistence
- Execute remote commands using PsExec
- Produce Indicators of Compromise (IOCs)
- Validate Splunk detections
- Support incident response investigations

---

# Attack Environment

| System | Role | IP Address |
|---------|------|------------|
| Kali-SOC | Attacker | 10.10.10.20 |
| Windows-SOC | Victim | 10.10.10.30 |
| Ubuntu-SOC | Splunk Enterprise | 10.10.10.10 |

---

# Attack Chain

```
Reconnaissance
      │
      ▼
Host Discovery
      │
      ▼
Account Enumeration
      │
      ▼
System Discovery
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
Threat Hunting
```

---

# Attack Stages

## Stage 1 – System Discovery

The attacker gathered information about the target host.

Commands executed:

```cmd
whoami
hostname
systeminfo
ipconfig
```

Purpose:

- Identify current user
- Obtain hostname
- Enumerate operating system
- Discover network configuration

MITRE ATT&CK:

- T1033 – System Owner/User Discovery
- T1082 – System Information Discovery
- T1016 – System Network Configuration Discovery

Expected Telemetry:

- Sysmon Event ID 1
- Process Creation
- CommandLine
- ParentImage

---

## Stage 2 – Account Discovery

Commands:

```cmd
net user

net localgroup administrators

net localgroup "Remote Desktop Users"
```

Purpose:

Identify privileged accounts and potential lateral movement targets.

MITRE:

- T1087
- T1069

---

## Stage 3 – Process Discovery

Commands

```cmd
tasklist

sc query

schtasks /query
```

Purpose

Identify running processes, services and scheduled tasks.

MITRE

- T1057
- T1007
- T1053

---

## Stage 4 – Registry Discovery

Commands

```cmd
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run

reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Purpose

Locate persistence mechanisms already present on the endpoint.

MITRE

T1012

---

## Stage 5 – Registry Persistence

Registry key created:

```
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Value

```
ChromeUpdater
```

Payload

```
payload.bat
```

Purpose

Simulate Registry Run Key persistence.

MITRE

T1547.001

---

## Stage 6 – Scheduled Task Persistence

Task

```
ChromeUpdate
```

Trigger

```
ONLOGON
```

Payload

```
payload.bat
```

Purpose

Simulate attacker persistence.

MITRE

T1053.005

---

## Stage 7 – Remote Execution

Remote shell established using:

- Impacket PsExec

Commands executed remotely:

```cmd
hostname

whoami

systeminfo

ipconfig

tasklist

reg query

schtasks /query
```

Purpose

Simulate post-compromise lateral movement.

MITRE

T1569.002

---

## Stage 8 – IOC Generation

The attack intentionally generated the following artifacts:

- payload.bat
- ChromeUpdater
- ChromeUpdate
- reg.exe
- schtasks.exe
- tasklist.exe
- systeminfo.exe
- whoami.exe
- hostname.exe

These indicators were later used during threat hunting.

---

# Telemetry Generated

The following telemetry was collected:

- Process Creation
- Parent/Child Relationships
- Registry Access
- Registry Modification
- Scheduled Task Creation
- Remote Process Execution
- Command Line Logging

---

# Detection Opportunities

This attack chain enables detection of:

- Discovery commands
- Registry modifications
- Persistence creation
- Scheduled task creation
- PsExec activity
- IOC searches
- Timeline reconstruction

---

# MITRE ATT&CK Coverage

| Technique | ATT&CK ID |
|------------|-----------|
| User Discovery | T1033 |
| System Discovery | T1082 |
| Network Discovery | T1016 |
| Account Discovery | T1087 |
| Group Discovery | T1069 |
| Process Discovery | T1057 |
| Service Discovery | T1007 |
| Registry Discovery | T1012 |
| Registry Persistence | T1547.001 |
| Scheduled Task | T1053.005 |
| Remote Service Execution | T1569.002 |

---

# Screenshots

| Screenshot | Description |
|------------|-------------|
| 20 | Discovery Simulation |
| 21 | Account Discovery |
| 22 | Process Discovery |
| 23 | Registry Discovery |
| 24 | Registry Persistence |
| 25 | Payload Creation |
| 26 | Scheduled Task |
| 27 | PsExec Session |
| 28 | Sysmon Telemetry |
| 29 | IOC Hunt |
| 30 | Timeline |
| 31 | MITRE Mapping |
| 32 | Detection Summary |

---

# Phase Outcome

This phase successfully simulated a realistic Windows intrusion workflow, including host discovery, account enumeration, persistence establishment, remote command execution, and IOC generation. The generated telemetry was captured through Sysmon and analyzed within Splunk Enterprise, providing high-quality data for detection engineering, threat hunting, and incident response activities.