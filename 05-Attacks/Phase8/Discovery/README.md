# Discovery Phase

## Overview

The Discovery phase simulates the actions performed by an attacker immediately after gaining access to a Windows endpoint. The objective is to collect information about the compromised system, identify privileged accounts, enumerate services, and understand the operating environment before moving to persistence or lateral movement.

This activity generates valuable endpoint telemetry that can be detected using Sysmon and analyzed in Splunk.

---

# Objective

The objectives of this stage were to:

- Identify the current user
- Determine the hostname
- Collect operating system information
- Identify network configuration
- Enumerate local users
- Identify privileged groups
- Enumerate running processes
- Enumerate Windows services
- Enumerate scheduled tasks

---

# Target

| Host | Windows-SOC |
|------|-------------|
| IP Address | 10.10.10.30 |

---

# Commands Executed

## User Discovery

```cmd
whoami
```

Purpose

Identify the compromised user account.

MITRE ATT&CK

T1033 – System Owner/User Discovery

---

## Host Discovery

```cmd
hostname
```

Purpose

Identify the hostname.

MITRE

T1082 – System Information Discovery

---

## System Information

```cmd
systeminfo
```

Purpose

Collect operating system information.

MITRE

T1082

---

## Network Configuration

```cmd
ipconfig /all
```

Purpose

Collect network information.

MITRE

T1016 – System Network Configuration Discovery

---

## Local Users

```cmd
net user
```

Purpose

Enumerate local user accounts.

MITRE

T1087 – Account Discovery

---

## Administrator Group

```cmd
net localgroup administrators
```

Purpose

Identify privileged users.

MITRE

T1069 – Permission Group Discovery

---

## Remote Desktop Users

```cmd
net localgroup "Remote Desktop Users"
```

Purpose

Identify users capable of remote access.

MITRE

T1069

---

## Running Processes

```cmd
tasklist
```

Purpose

Enumerate active processes.

MITRE

T1057 – Process Discovery

---

## Windows Services

```cmd
sc query
```

Purpose

Enumerate services.

MITRE

T1007 – System Service Discovery

---

## Scheduled Tasks

```cmd
schtasks /query
```

Purpose

Enumerate scheduled tasks.

MITRE

T1053.005

---

# Telemetry Generated

The following Sysmon telemetry was generated:

- Process Creation (Event ID 1)
- Parent Process
- Command Line
- User Context
- Process Hashes

---

# Detection Opportunities

The following detections were validated:

- Discovery Commands
- Account Enumeration
- Process Enumeration
- Service Enumeration
- Scheduled Task Enumeration

---

# Splunk Search

```spl
index=sysmon earliest=-10m
(Image="*systeminfo.exe"
OR Image="*tasklist.exe"
OR Image="*schtasks.exe"
OR Image="*sc.exe"
OR Image="*net.exe"
OR Image="*net1.exe")
| table _time Computer User Image CommandLine ParentImage
| sort -_time
```

---

# Evidence

Screenshots:

- 20-discovery-systeminfo.png
- 21-account-discovery.png
- 22-process-service-discovery.png

---

# Outcome

The Discovery phase successfully simulated post-compromise host reconnaissance. The executed commands generated high-quality endpoint telemetry that was successfully collected by Sysmon and ingested into Splunk Enterprise. These events provide valuable indicators for threat hunting, detection engineering, and incident response investigations.