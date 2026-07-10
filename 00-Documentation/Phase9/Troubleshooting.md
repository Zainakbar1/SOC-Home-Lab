# Troubleshooting Guide

## Overview

This document consolidates the most common issues encountered during the development of the SOC Home Lab and documents the corresponding solutions. The issues described here were encountered during actual implementation and reflect realistic challenges faced when deploying SIEM platforms, configuring virtual networks, forwarding logs, and performing attack simulations.

---

# VMware Issues

## Problem 1 – Host-Only Adapter Not Working

### Symptoms

- Virtual machines could not communicate.
- Ping requests failed.
- Splunk Forwarder could not reach Ubuntu.

### Cause

Host-only adapter not configured correctly.

### Resolution

- Verified VMware Virtual Network Editor configuration.
- Assigned all virtual machines to the same Host-Only network.
- Configured static IP addresses.
- Restarted the virtual machines.

Status

✅ Resolved

---

## Problem 2 – Internet Not Working

### Symptoms

Ubuntu or Kali could not install packages.

### Cause

NAT adapter missing or disconnected.

### Resolution

- Enabled NAT adapter.
- Verified DHCP assignment.
- Confirmed Internet connectivity before proceeding.

Status

✅ Resolved

---

# Ubuntu Issues

## Problem 3 – SSH Connection Failed

### Symptoms

```
Connection refused
```

### Cause

OpenSSH Server not running.

### Resolution

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh
```

Status

✅ Resolved

---

## Problem 4 – Splunk Not Starting

### Symptoms

Splunk service failed to start.

### Cause

Incomplete installation or incorrect permissions.

### Resolution

```bash
sudo /opt/splunk/bin/splunk start
sudo /opt/splunk/bin/splunk enable boot-start
```

Verified:

```bash
sudo ss -tulpn | grep 8000
sudo ss -tulpn | grep 9997
```

Status

✅ Resolved

---

# Windows Issues

## Problem 5 – Sysmon Logs Missing

### Symptoms

No Sysmon events appeared in Splunk.

### Cause

- Sysmon not installed correctly.
- Incorrect configuration file.

### Resolution

Reinstall Sysmon:

```powershell
Sysmon64.exe -accepteula -i sysmonconfig.xml
```

Verify:

```powershell
Get-Service Sysmon64
```

Status

✅ Resolved

---

## Problem 6 – Splunk Universal Forwarder Not Sending Logs

### Symptoms

Windows endpoint not visible in Splunk.

### Cause

Forwarder configuration incorrect.

### Resolution

- Verified `outputs.conf`
- Verified forwarding port `9997`
- Restarted the Splunk Forwarder service

```powershell
Restart-Service SplunkForwarder
```

Status

✅ Resolved

---

## Problem 7 – Windows Firewall Blocking SMB

### Symptoms

SMB scans returned limited results.

### Cause

Windows Defender Firewall blocked inbound SMB traffic.

### Resolution

Enabled required firewall rules for controlled lab testing and verified connectivity.

Status

✅ Resolved

---

## Problem 8 – Hydra SMB Error

### Symptoms

```
invalid reply from target smb://10.10.10.30:445/
```

### Cause

Modern SMB implementations and Windows security settings are not fully compatible with Hydra's SMB module.

### Resolution

- Verified SMB connectivity with `nmap`.
- Used enumeration and telemetry generation instead of relying on Hydra.
- Focused on detection engineering rather than password guessing.

Status

✅ Documented (expected behavior)

---

# Kali Issues

## Problem 9 – SSH Connection Failed

### Symptoms

Unable to connect to Ubuntu.

### Resolution

Verified:

- IP address
- SSH service
- Host-only adapter
- Firewall settings

Status

✅ Resolved

---

## Problem 10 – Nmap Results Unexpected

### Symptoms

```
22/tcp filtered
```

### Cause

Firewall filtering or SSH service unavailable.

### Resolution

Verified SSH status and firewall configuration before repeating the scan.

Status

✅ Resolved

---

# Splunk Issues

## Problem 11 – No Search Results

### Symptoms

Search returned:

```
No results found
```

### Cause

- Incorrect index
- Wrong time range
- Forwarder not sending logs

### Resolution

Verified:

- Index selection
- Time picker
- Splunk inputs
- Forwarder status

Status

✅ Resolved

---

## Problem 12 – Detection Query Returned Unexpected Results

### Cause

Legitimate administrator activity matched the search criteria.

### Resolution

Improved query tuning by:

- Filtering known administrative processes
- Reviewing parent-child process relationships
- Adding IOC-specific conditions

Status

✅ Resolved

---

# Threat Hunting Issues

## Problem 13 – Missing IOC

### Symptoms

Expected IOC not found.

### Cause

Telemetry had not yet been ingested or incorrect search window selected.

### Resolution

- Expanded the search time range.
- Verified Sysmon process creation events.
- Confirmed Splunk ingestion.

Status

✅ Resolved

---

## Problem 14 – Timeline Incomplete

### Cause

Search did not include all relevant processes.

### Resolution

Expanded SPL query to include:

- Discovery commands
- Registry activity
- Scheduled tasks
- Payload references

Status

✅ Resolved

---

# Incident Response Issues

## Problem 15 – No Security Event ID 4720

### Symptoms

```
No events were found that match the specified selection criteria.
```

### Cause

No local user account had been created during the simulation, and advanced auditing was not configured to generate this event.

### Resolution

Documented the limitation and relied on available Sysmon telemetry for the investigation.

Status

✅ Expected Behavior

---

# General Lessons

Throughout the project the following best practices proved valuable:

- Create VMware snapshots before major changes.
- Validate network connectivity before troubleshooting applications.
- Verify Sysmon operation before investigating Splunk.
- Confirm Splunk log ingestion before writing detection rules.
- Test detection queries using known attacker activity.
- Document every issue and its resolution.

---

# Recommended Troubleshooting Workflow

```
VMware
    │
    ▼
Network
    │
    ▼
Operating System
    │
    ▼
Sysmon
    │
    ▼
Splunk Forwarder
    │
    ▼
Splunk Enterprise
    │
    ▼
Detection Rules
    │
    ▼
Threat Hunting
```

---

# Conclusion

The SOC Home Lab was successfully completed despite encountering common infrastructure, networking, telemetry, and detection challenges. Each issue was systematically investigated, documented, and resolved using standard troubleshooting techniques. This guide provides a reference for future deployments and demonstrates practical experience in diagnosing and resolving real-world operational problems within a SOC environment.