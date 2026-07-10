# Phase 08 – Detection Engineering

## Overview

This phase focuses on developing and validating detection logic for attacker techniques executed during Phase 8 of the SOC Home Lab.

Detection engineering transforms raw endpoint telemetry into actionable security detections. Using Sysmon telemetry collected from the Windows endpoint and centralized within Splunk Enterprise, custom Splunk Search Processing Language (SPL) queries were developed to detect discovery activity, persistence mechanisms, remote execution, and attacker indicators of compromise.

The detections created during this phase are designed to emulate SOC monitoring workflows and demonstrate practical blue-team capabilities.

---

# Objectives

The objectives of this phase were to:

- Develop Splunk detection queries
- Detect attacker discovery activity
- Detect Registry persistence
- Detect Scheduled Task persistence
- Detect remote execution
- Perform IOC hunting
- Validate MITRE ATT&CK mappings
- Create SOC correlation searches
- Create security alerts
- Validate detections using simulated attacker activity

---

# Detection Environment

| Component | Description |
|-----------|-------------|
| SIEM | Splunk Enterprise 10.4 |
| Endpoint | Windows 11 |
| Telemetry | Sysmon |
| Log Forwarder | Splunk Universal Forwarder |
| Attacker | Kali Linux |

---

# Data Sources

Detection engineering relied on the following telemetry:

- Sysmon Process Creation (Event ID 1)
- Windows Event Logs
- Registry Activity
- Scheduled Task Activity
- Command Line Logging
- Parent Process Information
- User Context

---

# Detection Categories

## Discovery Detection

Purpose

Detect common attacker discovery commands.

Examples:

- whoami
- hostname
- systeminfo
- ipconfig
- tasklist
- net user
- sc query
- schtasks

---

## Registry Persistence Detection

Purpose

Detect Registry Run Key modifications.

Indicators:

- reg.exe
- CurrentVersion\Run
- ChromeUpdater

---

## Scheduled Task Detection

Purpose

Detect creation of malicious scheduled tasks.

Indicators:

- schtasks.exe
- ChromeUpdate
- payload.bat

---

## IOC Hunting

Purpose

Locate attacker artifacts.

Indicators:

- payload.bat
- ChromeUpdater
- ChromeUpdate
- reg.exe
- schtasks.exe

---

## Timeline Detection

Purpose

Reconstruct attacker activity.

Fields:

- Time
- Parent Process
- Process
- User
- Command Line

---

## MITRE Mapping

The following ATT&CK techniques were successfully detected.

| Technique | ATT&CK ID |
|-----------|-----------|
| User Discovery | T1033 |
| System Discovery | T1082 |
| Network Discovery | T1016 |
| Account Discovery | T1087 |
| Permission Group Discovery | T1069 |
| Process Discovery | T1057 |
| Service Discovery | T1007 |
| Registry Discovery | T1012 |
| Registry Run Key | T1547.001 |
| Scheduled Task | T1053.005 |
| Remote Service Execution | T1569.002 |

---

# Detection Files

## Queries

- Discovery.spl
- RegistryPersistence.spl
- SchedulerTasks.spl
- IOC-Hunt.spl
- AttackTimeline.spl
- MITRE-Persistence.spl
- DetectionSummary.spl

---

## Correlation Searches

- Discovery Detection
- Persistence Detection
- Threat Hunt

---

## Alerts

- Registry Persistence Alert
- Scheduled Task Alert

---

# Validation

Each detection query was validated against live telemetry generated during attack simulation.

Successful detections included:

- Discovery Commands
- Registry Modifications
- Registry Persistence
- Scheduled Task Creation
- IOC Searches
- Timeline Reconstruction
- Remote Execution

---

# Screenshots

The following screenshots demonstrate successful validation of detection engineering.

20–32

---

# Skills Demonstrated

- Detection Engineering
- Splunk SPL
- Sysmon Analysis
- Threat Hunting
- IOC Hunting
- ATT&CK Mapping
- Windows Forensics
- SOC Monitoring
- Endpoint Detection
- Security Analytics

---

# Phase Outcome

Phase 8 successfully demonstrated the complete detection engineering lifecycle, beginning with attacker simulation and ending with validated Splunk detections. Custom SPL searches successfully identified discovery activity, Registry persistence, Scheduled Task persistence, remote execution, and Indicators of Compromise. These detections form the foundation for SOC monitoring, correlation searches, and incident response workflows.