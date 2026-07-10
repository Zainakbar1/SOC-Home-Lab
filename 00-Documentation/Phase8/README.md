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
   Ubuntu SOC         Kali Linux        Windows 11
   10.10.10.10        10.10.10.20       10.10.10.30
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

![Initial Incident Assessment](../Screenshots/Phase8/01-initial-incident-assessment.png)
*Figure 1: Initial assessment verifying that no malicious process or shell session is currently running.*

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

![Sysmon Evidence](../Screenshots/Phase8/02-sysmon-evidence.png)
*Figure 2: Process creation events logged in Sysmon.*

![Service Installation Events](../Screenshots/Phase8/03-service-installation-events.png)
*Figure 3: New service installations detected in the logs.*

![Local Administrators](../Screenshots/Phase8/04-local-administrators.png)
*Figure 4: Active accounts list indicating local administrative changes.*

![Scheduled Tasks](../Screenshots/Phase8/05-scheduled-tasks.png)
*Figure 5: Active scheduled tasks listing.*

![Services Verification](../Screenshots/Phase8/06-services-verification.png)
*Figure 6: Active system services verification output.*

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

![Startup Folder](../Screenshots/Phase8/07-startup-folder.png)
*Figure 7: Checking startup directory content.*

![Registry Run HKLM](../Screenshots/Phase8/08-registry-run-hklm.png)
*Figure 8: Local machine Run keys query results.*

![Registry Run HKCU](../Screenshots/Phase8/09-registry-run-hkcu.png)
*Figure 9: Current user Run keys query results.*

![Local Users](../Screenshots/Phase8/10-local-users.png)
*Figure 10: Local users listing.*

![User Creation Events](../Screenshots/Phase8/11-user-creation-events.png)
*Figure 11: Event ID 4720 logging user creation.*

![RDP Users](../Screenshots/Phase8/12-rdp-users.png)
*Figure 12: Remote desktop users list.*

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

![Attack Timeline](../Screenshots/Phase8/13-attack-timeline.png)
*Figure 13: Splunk search reconstructing the full attack timeline.*

![PsExec Events](../Screenshots/Phase8/14-psexec-events.png)
*Figure 14: Filtering for PsExec process creation telemetry.*

![SMB Activity](../Screenshots/Phase8/15-smb-activity.png)
*Figure 15: Mapping SMB connection events.*

![Service Install](../Screenshots/Phase8/16-service-install.png)
*Figure 16: Finding Event ID 7045 service install logs.*

![Logons](../Screenshots/Phase8/17-logons.png)
*Figure 17: Analyzing logon events for administrative users.*

![Process Tree](../Screenshots/Phase8/18-process-tree.png)
*Figure 18: Generating the execution process tree in Splunk.*

![IOCs](../Screenshots/Phase8/19-iocs.png)
*Figure 19: Finding specific Indicators of Compromise.*

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

![Discovery Systeminfo](../Screenshots/Phase8/20-discovery-systeminfo.png)
*Figure 20: Attacker executing systeminfo to profile target.*

![Account Discovery](../Screenshots/Phase8/21-account-discovery.png)
*Figure 21: Attacker running net user to list active accounts.*

![Process Service Discovery](../Screenshots/Phase8/22-process-service-discovery.png)
*Figure 22: Attacker listing services and processes.*

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

![Registry Discovery](../Screenshots/Phase8/23-registry-discovery.png)
*Figure 23: Attacker query of run key registry nodes.*

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

![Registry Persistence Created](../Screenshots/Phase8/24-registry-persistence-created.png)
*Figure 24: Sysmon capturing registry key modification for persistence.*

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

![Payload Created](../Screenshots/Phase8/25-payload-created.png)
*Figure 25: Payload batch script placed in the endpoint filesystem.*

![Scheduled Task Created](../Screenshots/Phase8/26-scheduled-task-created.png)
*Figure 26: Creation of scheduled task 'ChromeUpdate' recorded in logs.*

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

![PsExec Session](../Screenshots/Phase8/27-psexec-session.png)
*Figure 27: Attacker remote console execution session.*

![PsExec Sysmon Events](../Screenshots/Phase8/28-psexec-sysmon-events.png)
*Figure 28: Endpoint logs indicating psexecsvc.exe service operations.*

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

![Final IOC Hunt](../Screenshots/Phase8/29-final-ioc-hunt.png)
*Figure 29: Splunk query isolating specific malware indicators.*

---

## Step 11 – Timeline Reconstruction

Splunk was used to reconstruct the complete attack timeline.

Fields analyzed:

- Timestamp
- Parent Process
- Process
- User
- Command Line

![Attack Timeline Reconstruction](../Screenshots/Phase8/30-attack-timeline.png)
*Figure 30: Detailed event-by-event timeline search in Splunk.*

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

![MITRE Persistence](../Screenshots/Phase8/31-mitre-persistence.png)
*Figure 31: Mapping malicious registry key additions to MITRE T1547.001.*

---

## Step 13 – Detection Validation

Detection rules successfully identified:

- Discovery activity
- Registry modifications
- Scheduled task creation
- IOC activity
- Timeline reconstruction

![Detection Summary](../Screenshots/Phase8/32-detection-summary.png)
*Figure 32: Summary of successfully triggered correlation rules in Splunk.*

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