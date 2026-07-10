# Sysmon Configuration

## Overview

This directory contains the Sysmon configuration and documentation used in the SOC Home Lab.

Sysmon (System Monitor) is a Microsoft Sysinternals utility that extends Windows event logging by generating detailed telemetry about system activity. The collected events are forwarded to Splunk Enterprise through the Splunk Universal Forwarder, providing the visibility required for detection engineering, threat hunting, and incident response.

---

# Objectives

The objectives of deploying Sysmon in this project were:

- Monitor process creation
- Capture network connections
- Record registry modifications
- Detect service installation
- Monitor scheduled task creation
- Record file creation events
- Provide endpoint telemetry for Splunk Enterprise
- Support MITRE ATT&CK mapping

---

# Environment

| Component | Value |
|-----------|-------|
| Host | Windows-SOC |
| Operating System | Windows 11 |
| Monitoring Tool | Sysmon |
| Configuration | SwiftOnSecurity Sysmon Config (Customized) |
| Log Collector | Splunk Universal Forwarder |
| SIEM | Splunk Enterprise |

---

# Directory Structure

```
04-Sysmon/
│
├── README.md
└── Configs/
    └── sysmonconfig-export.xml
```

---

# Installation

Sysmon was installed using the Sysinternals executable and a customized XML configuration.

Example installation command:

```powershell
Sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

To update the configuration:

```powershell
Sysmon64.exe -c sysmonconfig-export.xml
```

To uninstall:

```powershell
Sysmon64.exe -u
```

---

# Log Location

Sysmon events are stored in the Windows Event Log:

```
Applications and Services Logs
    └── Microsoft
        └── Windows
            └── Sysmon
                └── Operational
```

---

# Event Collection Workflow

```
Windows Endpoint
        │
        ▼
Sysmon
        │
        ▼
Windows Event Log
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Enterprise
```

---

# Important Event IDs

| Event ID | Description |
|----------|-------------|
| 1 | Process Creation |
| 2 | File Creation Time Changed |
| 3 | Network Connection |
| 5 | Process Terminated |
| 7 | Image Loaded |
| 8 | Create Remote Thread |
| 10 | Process Access |
| 11 | File Create |
| 12 | Registry Object Create/Delete |
| 13 | Registry Value Set |
| 14 | Registry Object Rename |
| 15 | FileCreateStreamHash |
| 17 | Pipe Created |
| 18 | Pipe Connected |
| 19 | WMI Event Filter |
| 20 | WMI Event Consumer |
| 21 | WMI Event Binding |
| 22 | DNS Query |
| 23 | File Delete |
| 24 | Clipboard Change |
| 25 | Process Tampering |
| 26 | File Delete Detected |
| 255 | Sysmon Error |

---

# Events Used During This Project

The following Sysmon events were actively used during the SOC Home Lab:

- Event ID 1 – Process Creation
- Event ID 3 – Network Connections
- Event ID 11 – File Creation
- Event ID 12 – Registry Key Creation
- Event ID 13 – Registry Value Modification
- Event ID 22 – DNS Queries

These events formed the basis for custom Splunk detection rules and threat hunting investigations.

---

# Detection Use Cases

Sysmon telemetry enabled detection of:

- Nmap reconnaissance
- SMB enumeration
- PsExec remote execution
- Registry Run Key persistence
- Scheduled Task persistence
- Suspicious process execution
- Service installation
- IOC generation

---

# MITRE ATT&CK Coverage

Examples of techniques observed during the project:

| Technique | ID |
|-----------|----|
| System Information Discovery | T1082 |
| Account Discovery | T1087 |
| Process Discovery | T1057 |
| Registry Discovery | T1012 |
| Registry Run Keys / Startup Folder | T1547.001 |
| Scheduled Task | T1053.005 |
| Remote Services | T1021 |
| Service Execution | T1569.002 |

---

# Verification

Verify Sysmon installation:

```powershell
Get-Service Sysmon64
```

View recent events:

```powershell
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -MaxEvents 10
```

---

# Related Documentation

- `03-Splunk`
- `05-Attacks`
- `06-Detections`
- `07-Incident-Reports`
- `10-MITRE`

---

# Conclusion

Sysmon served as the primary endpoint telemetry source throughout the SOC Home Lab. By capturing detailed Windows activity and forwarding it to Splunk Enterprise, it enabled realistic detection engineering, threat hunting, and incident response workflows aligned with industry best practices.