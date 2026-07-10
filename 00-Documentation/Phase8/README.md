# Phase 08 – Incident Response, Threat Hunting & Detection Engineering

## Phase Overview

This phase focuses on post-compromise investigation, incident response, threat hunting, and detection engineering within the SOC Home Lab. Building on the attack simulations completed in Phases 6 and 7, this phase shifts perspective from the attacker to the defender.

The primary objective is to investigate attacker activity using endpoint telemetry collected by Sysmon and centralized within Splunk Enterprise. Through systematic analysis, indicators of compromise (IOCs) are identified, persistence mechanisms are investigated, attack timelines are reconstructed, and malicious activity is mapped to the MITRE ATT&CK Framework.

This phase demonstrates the workflow followed by a Security Operations Center (SOC) analyst when responding to an endpoint compromise.

---

# Objectives

At the completion of this phase, the following objectives were achieved:

- Perform endpoint incident investigation
- Collect forensic evidence
- Validate persistence mechanisms
- Hunt for attacker artifacts
- Investigate registry modifications
- Investigate scheduled task persistence
- Analyze Sysmon telemetry
- Perform IOC hunting using Splunk
- Reconstruct attacker timeline
- Validate detection engineering rules
- Map observed activity to MITRE ATT&CK
- Produce evidence suitable for incident reporting

---

# Lab Topology

```
                    Internet
                        │
                 VMware NAT Network
                        │
        ┌───────────────┼───────────────┐
        │               │               │
        │               │               │
 Ubuntu SOC         Kali Linux      Windows 11
10.10.10.10        10.10.10.20      10.10.10.30
        │               │               │
        └────── Host-Only SOC Network ──┘
```

---

# Systems Used

| Machine | Role | IP Address |
|----------|------|------------|
| Ubuntu-SOC | Splunk Enterprise | 10.10.10.10 |
| Kali-SOC | Attacker | 10.10.10.20 |
| Windows-SOC | Victim | 10.10.10.30 |

---

# Software Used

- VMware Workstation Pro
- Ubuntu 26.04 LTS
- Windows 11
- Kali Linux
- Splunk Enterprise 10.4
- Splunk Universal Forwarder
- Sysmon
- PowerShell
- PsExec (Impacket)
- NetExec
- Nmap

---

# Phase Workflow

The investigation followed the NIST Incident Response Lifecycle.

```
Preparation
      │
      ▼
Identification
      │
      ▼
Evidence Collection
      │
      ▼
Threat Hunting
      │
      ▼
Containment Validation
      │
      ▼
Recovery Verification
      │
      ▼
Lessons Learned
```

---

# Implementation

## Step 1 – Initial Incident Assessment

The Windows endpoint was examined to determine whether the attacker remained active.

Validation included:

- Logged-on users
- Running services
- PsExec service verification
- Active SMB sessions
- Current processes

Commands executed:

```powershell
whoami
hostname
Get-Service PSEXESVC
Get-Process
net session
quser
```

Result:

- No active PsExec service
- No active SMB sessions
- Sysmon operational
- Splunk Forwarder operational
- Windows Defender operational

Screenshot:

```
01-initial-incident-assessment.png
```

---

## Step 2 – Evidence Collection

Endpoint telemetry was collected using Sysmon and Windows Event Logs.

Evidence gathered included:

- Process Creation
- Service Installation
- Local Administrator membership
- Scheduled Tasks
- Running Services

PowerShell Commands

```powershell
Get-WinEvent
Get-Service
Get-LocalUser
Get-ScheduledTask
```

Screenshots

02–06

---

## Step 3 – Persistence Verification

The endpoint was examined for common persistence mechanisms.

Validated:

- Startup Folder
- Registry Run Keys
- Local Users
- Event ID 4720
- Remote Desktop Users

Result:

No unauthorized persistence mechanisms were discovered.

Screenshots

07–12

---

## Step 4 – Splunk Investigation

Threat hunting activities were performed using Splunk Enterprise.

Searches included:

- Attack Timeline
- PsExec Activity
- SMB Activity
- Process Tree
- IOC Search
- Service Installation
- Logon Events

Screenshots

13–19

---

## Step 5 – Advanced Discovery Simulation

A realistic attacker discovery sequence was executed to generate endpoint telemetry.

Commands executed included:

```cmd
hostname
whoami
systeminfo
ipconfig
net user
tasklist
sc query
schtasks
```

Telemetry generated:

- Sysmon Event ID 1
- Parent Process
- Command Line
- User Context

Screenshots

20–22

---

## Step 6 – Registry Investigation

Registry Run Keys were inspected.

Commands

```cmd
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
```

Purpose

Detect Registry-based persistence.

Screenshot

23

---

## Step 7 – Registry Persistence Simulation

A fake Registry Run Key was created.

Command

```cmd
reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Persistence Name

```
ChromeUpdater
```

Target

```
payload.bat
```

Detection

Successfully captured by Sysmon and Splunk.

Screenshot

24

---

## Step 8 – Scheduled Task Persistence

A scheduled task was created.

Task Name

```
ChromeUpdate
```

Trigger

```
ONLOGON
```

Execution

```
payload.bat
```

Detection

Successfully captured by Splunk.

Screenshots

25–26

---

## Step 9 – Remote Execution

Impacket PsExec was used to simulate lateral movement.

Commands executed remotely:

- hostname
- whoami
- systeminfo
- ipconfig
- tasklist
- sc query
- reg query
- schtasks

Telemetry generated:

- Process Creation
- Parent Process
- SYSTEM Context
- Command Line

Screenshots

27–28

---

## Step 10 – IOC Hunting

Splunk searches were used to locate attacker artifacts.

Indicators searched:

- payload.bat
- ChromeUpdate
- Registry Run Keys
- reg.exe
- schtasks.exe
- systeminfo.exe
- tasklist.exe

Screenshots

29

---

## Step 11 – Timeline Reconstruction

Splunk was used to reconstruct the complete attack timeline.

Fields analyzed:

- Timestamp
- Parent Process
- Process
- User
- Command Line

Screenshot

30

---

## Step 12 – MITRE ATT&CK Mapping

Observed techniques were mapped to MITRE ATT&CK.

| Activity | ATT&CK |
|----------|---------|
| User Discovery | T1033 |
| System Discovery | T1082 |
| Account Discovery | T1087 |
| Process Discovery | T1057 |
| Service Discovery | T1007 |
| Registry Discovery | T1012 |
| Registry Persistence | T1547.001 |
| Scheduled Tasks | T1053.005 |
| Remote Execution | T1569.002 |

Screenshot

31

---

## Step 13 – Detection Validation

Detection rules successfully identified:

- Discovery activity
- Registry modifications
- Scheduled task creation
- IOC activity
- Timeline reconstruction

Screenshot

32

---

# Phase Screenshots

| Screenshot | Description |
|------------|-------------|
| 01 | Initial Incident Assessment |
| 02–06 | Evidence Collection |
| 07–12 | Persistence Verification |
| 13–19 | Splunk Investigation |
| 20–22 | Discovery Simulation |
| 23 | Registry Discovery |
| 24 | Registry Persistence |
| 25 | Payload Creation |
| 26 | Scheduled Task Creation |
| 27 | PsExec Session |
| 28 | Remote Telemetry |
| 29 | IOC Hunt |
| 30 | Attack Timeline |
| 31 | MITRE Mapping |
| 32 | Detection Summary |

---

# Skills Demonstrated

- Incident Response
- Threat Hunting
- Detection Engineering
- Splunk SPL
- Sysmon Analysis
- Windows Forensics
- IOC Collection
- Timeline Reconstruction
- MITRE ATT&CK Mapping
- Endpoint Investigation
- Persistence Detection
- Lateral Movement Analysis

---

# Phase Outcome

Phase 8 successfully demonstrated a complete post-compromise investigation within the SOC Home Lab. Endpoint telemetry generated during simulated attacker activity was collected through Sysmon, centralized in Splunk Enterprise, and analyzed using threat hunting methodologies. Registry persistence, scheduled task persistence, discovery commands, and remote execution artifacts were successfully identified, enabling reconstruction of the attack timeline and validation of detection capabilities. This phase demonstrates the practical responsibilities of a SOC Analyst performing endpoint investigation, threat hunting, and incident response.