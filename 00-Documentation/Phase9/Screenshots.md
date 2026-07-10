# Project Screenshot Index

## Overview

This document serves as the master index for all screenshots collected throughout the SOC Home Lab project.

Screenshots were captured during each implementation phase to provide visual evidence of completed configurations, attack simulations, detection engineering, threat hunting, and incident response activities.

The screenshots are organized chronologically by project phase and can be used to verify successful implementation of each task.

---

# Screenshot Standards

Each screenshot captures one or more of the following:

- Successful command execution
- Configuration changes
- VMware configuration
- Splunk dashboards
- Detection results
- Sysmon events
- Attack simulations
- Threat hunting investigations
- Incident response evidence

Naming convention:

```
PhaseX-XX-Description.png
```

Example:

```
Phase6-05-SMB-Detection.png
```

---

# Phase 0 – Lab Planning

## Screenshots

| Screenshot | Description |
|------------|-------------|
| Phase0-01 | VMware Workstation Installation |
| Phase0-02 | Virtual Network Configuration |
| Phase0-03 | ISO Downloads |
| Phase0-04 | VM Folder Structure |
| Phase0-05 | Initial Project Layout |

---

# Phase 1 – Ubuntu SOC Server

| Screenshot | Description |
|------------|-------------|
| Phase1-01 | Ubuntu Installation |
| Phase1-02 | Network Configuration |
| Phase1-03 | SSH Verification |
| Phase1-04 | System Updates |
| Phase1-05 | Static IP Configuration |
| Phase1-06 | VMware Snapshot |

---

# Phase 2 – Splunk Deployment

| Screenshot | Description |
|------------|-------------|
| Phase2-01 | Splunk Installation |
| Phase2-02 | Splunk Login |
| Phase2-03 | Index Creation |
| Phase2-04 | Receiving Port Configuration |
| Phase2-05 | Splunk Status |
| Phase2-06 | Splunk Dashboard |

---

# Phase 3 – Windows Logging

| Screenshot | Description |
|------------|-------------|
| Phase3-01 | Windows Installation |
| Phase3-02 | Sysmon Installation |
| Phase3-03 | Splunk Universal Forwarder |
| Phase3-04 | Event Logs |
| Phase3-05 | Log Ingestion |
| Phase3-06 | Sysmon Verification |

---

# Phase 4 – Kali Linux

| Screenshot | Description |
|------------|-------------|
| Phase4-01 | Kali Installation |
| Phase4-02 | Network Configuration |
| Phase4-03 | Tool Installation |
| Phase4-04 | Connectivity Tests |
| Phase4-05 | Attack Platform Ready |

---

# Phase 5 – Attack Simulation

| Screenshot | Description |
|------------|-------------|
| Phase5-01 | Nmap Scan |
| Phase5-02 | SMB Enumeration |
| Phase5-03 | Service Enumeration |
| Phase5-04 | Hydra Testing |
| Phase5-05 | Initial Attack Validation |

---

# Phase 6 – Detection Engineering

| Screenshot | Description |
|------------|-------------|
| Phase6-01 | Splunk Search |
| Phase6-02 | SMB Detection |
| Phase6-03 | Detection Validation |
| Phase6-04 | MITRE Mapping |
| Phase6-05 | Incident Detection |
| Phase6-06 | Detection Dashboard |

---

# Phase 7 – Threat Hunting

| Screenshot | Description |
|------------|-------------|
| Phase7-01 | Threat Hunt Initiated |
| Phase7-02 | Discovery Activity |
| Phase7-03 | Process Investigation |
| Phase7-04 | Registry Investigation |
| Phase7-05 | Timeline Analysis |
| Phase7-06 | Hunt Results |

---

# Phase 8 – Incident Response

## Initial Assessment

| Screenshot | Description |
|------------|-------------|
| 01 | Initial Incident Assessment |
| 02 | Running Services |
| 03 | Running Processes |
| 04 | Logged-on Users |
| 05 | SMB Sessions |
| 06 | Initial Evidence Collection |

---

## Persistence Verification

| Screenshot | Description |
|------------|-------------|
| 07 | Startup Folder |
| 08 | Registry Run Keys |
| 09 | Local Users |
| 10 | Remote Desktop Users |
| 11 | Security Event Review |
| 12 | Persistence Verification Complete |

---

## Splunk Investigation

| Screenshot | Description |
|------------|-------------|
| 13 | Discovery Search |
| 14 | Sysmon Events |
| 15 | Process Tree |
| 16 | Parent-Child Analysis |
| 17 | IOC Search |
| 18 | Timeline Query |
| 19 | Detection Validation |

---

## Attack Simulation

| Screenshot | Description |
|------------|-------------|
| 20 | Discovery Commands |
| 21 | Account Enumeration |
| 22 | Process & Service Discovery |

---

## Persistence Simulation

| Screenshot | Description |
|------------|-------------|
| 23 | Registry Discovery |
| 24 | Registry Run Key Creation |
| 25 | Payload Creation |
| 26 | Scheduled Task Creation |

---

## Remote Execution

| Screenshot | Description |
|------------|-------------|
| 27 | PsExec Session |
| 28 | Remote Command Execution |

---

## Threat Hunting

| Screenshot | Description |
|------------|-------------|
| 29 | IOC Hunt |
| 30 | Timeline Reconstruction |
| 31 | MITRE ATT&CK Mapping |
| 32 | Detection Summary |

---

# Total Project Statistics

| Category | Count |
|-----------|------:|
| Project Phases | 9 |
| Total Screenshots | 100+ |
| VMware Snapshots | 7 |
| Detection Rules | 20+ |
| SPL Queries | 7 |
| Incident Reports | 5 |

---

# Screenshot Guidelines

All screenshots should:

- Display the full application window where practical.
- Include timestamps when available.
- Clearly show successful command execution or configuration.
- Avoid exposing sensitive credentials.
- Be stored using the project's naming convention.
- Be committed alongside the corresponding phase documentation.

---

# Portfolio Usage

These screenshots provide visual evidence supporting:

- VMware configuration
- Ubuntu server deployment
- Splunk implementation
- Windows endpoint logging
- Kali attack simulation
- Detection engineering
- Threat hunting
- Incident response
- MITRE ATT&CK mapping

They can be referenced during technical interviews, included in project presentations, or used to demonstrate practical SOC analyst skills.

---

# Conclusion

The screenshot collection documents the complete lifecycle of the SOC Home Lab, from initial infrastructure deployment to incident response. Organized by phase and standardized with a consistent naming convention, the collection serves as a comprehensive visual record of the project and supports the accompanying technical documentation.