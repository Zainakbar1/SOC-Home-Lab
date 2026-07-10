# Detection Engineering

## Overview

This directory contains the custom detection rules, Splunk Search Processing Language (SPL) queries, correlation searches, and alerts developed during the SOC Home Lab project.

The objective of this phase was to transform raw endpoint telemetry into actionable security detections capable of identifying attacker behavior, validating simulated attacks, and supporting threat hunting and incident response.

The detections are based on telemetry collected from Sysmon, Windows Event Logs, and the Splunk Universal Forwarder.

---

# Objectives

The goals of this phase were to:

- Develop custom Splunk SPL queries
- Detect simulated attacker activity
- Validate attack execution
- Map detections to MITRE ATT&CK
- Reduce false positives
- Support proactive threat hunting
- Build reusable detection logic

---

# Detection Workflow

```
Windows Endpoint
        │
        ▼
Sysmon
        │
        ▼
Windows Event Logs
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Enterprise
        │
        ▼
SPL Queries
        │
        ▼
Correlation Searches
        │
        ▼
Alerts
        │
        ▼
Threat Hunting
        │
        ▼
Incident Response
```

---

# Directory Structure

```
06-Detections/
│
├── README.md
│
├── Phase6
│   ├── Queries
│   ├── Correlation Searches
│   └── Alerts
│
├── Phase7
│   ├── Queries
│   ├── Correlation Searches
│   └── Alerts
│
└── Phase8
    ├── Queries
    ├── Correlation Searches
    └── Alerts
```

---

# Detection Categories

## Reconnaissance

Examples:

- Host Discovery
- Port Scanning
- Service Enumeration
- SMB Enumeration

---

## Credential Access

Examples:

- SMB Authentication
- Password Spraying
- Failed Authentication Monitoring

---

## Execution

Examples:

- PsExec
- Remote Process Creation
- Service Installation

---

## Persistence

Examples:

- Registry Run Keys
- Scheduled Tasks

---

## Threat Hunting

Examples:

- IOC Search
- Timeline Reconstruction
- Process Investigation
- Parent-Child Process Analysis

---

# SPL Queries

The repository includes custom SPL queries for:

- Process Creation
- Registry Persistence
- Scheduled Tasks
- SMB Authentication
- IOC Hunting
- Attack Timeline
- MITRE Mapping
- Detection Summary

---

# Correlation Searches

Correlation searches combine multiple events to identify suspicious behavior.

Examples include:

- Discovery Detection
- Persistence Detection
- PsExec Detection
- Threat Hunt Correlation
- SMB Authentication Monitoring

---

# Alerts

Custom alerts were created for:

- High Severity SMB Activity
- Registry Persistence
- Scheduled Task Creation

Alerts are intended to demonstrate SOC monitoring workflows rather than production tuning.

---

# MITRE ATT&CK Coverage

| Tactic | Technique |
|--------|-----------|
| Discovery | T1082 – System Information Discovery |
| Discovery | T1087 – Account Discovery |
| Discovery | T1057 – Process Discovery |
| Discovery | T1007 – Service Discovery |
| Discovery | T1012 – Registry Discovery |
| Credential Access | T1110 – Brute Force (Simulation) |
| Lateral Movement | T1021 – Remote Services |
| Execution | T1569.002 – Service Execution |
| Persistence | T1547.001 – Registry Run Keys |
| Persistence | T1053.005 – Scheduled Task |

---

# Data Sources

The detections use telemetry from:

- Sysmon
- Windows Security Logs
- Windows System Logs
- Windows Application Logs
- Splunk Universal Forwarder

---

# Validation

Every detection was validated using simulated attacker activity generated from the Kali Linux attack workstation.

Validation included:

- Confirming telemetry generation
- Executing SPL queries
- Reviewing search results
- Mapping detections to MITRE ATT&CK
- Documenting evidence with screenshots

---

# Related Directories

- `03-Splunk`
- `04-Sysmon`
- `05-Attacks`
- `07-Incident-Reports`
- `10-MITRE`

---

# Skills Demonstrated

This phase demonstrates practical experience in:

- Detection Engineering
- Splunk SPL
- Log Analysis
- Windows Security Monitoring
- MITRE ATT&CK Mapping
- Threat Hunting
- Incident Response Support

---

# Conclusion

The Detection Engineering phase transformed raw endpoint telemetry into meaningful security detections capable of identifying reconnaissance, credential access, execution, persistence, and lateral movement activities. These detections formed the foundation for the threat hunting and incident response exercises completed during later phases of the SOC Home Lab.