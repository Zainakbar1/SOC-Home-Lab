# Incident Report IR-003

## Incident Title

Remote Command Execution using Impacket PsExec

---

## Incident ID

IR-003

---

## Date

YYYY-MM-DD

---

## Severity

High

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Valid Accounts | T1078 |
| SMB/Windows Admin Shares | T1021.002 |
| Service Execution | T1569.002 |
| Windows Command Shell | T1059.003 |

---

# Executive Summary

A remote administrator session was established from the Kali attack workstation to the Windows endpoint using valid administrative credentials.

The attacker authenticated over SMB and executed commands remotely through Impacket PsExec.

Sysmon successfully recorded all process creation events.

---

# Affected Systems

| Host | IP |
|------|----|
| Kali-SOC | 10.10.10.20 |
| Windows-SOC | 10.10.10.30 |

---

# Attack Timeline

| Time | Activity |
|------|----------|
| T1 | SMB Authentication |
| T2 | ADMIN$ Share Access |
| T3 | PsExec Uploaded Binary |
| T4 | Temporary Service Created |
| T5 | Remote cmd.exe Started |
| T6 | whoami Executed |
| T7 | hostname Executed |
| T8 | ipconfig Executed |

---

# Evidence Collected

Evidence included:

- SMB Authentication
- NetExec Validation
- PsExec Execution
- Sysmon Event ID 1
- Process Creation Logs
- Splunk Search Results

---

# Indicators of Compromise

Source IP

```
10.10.10.20
```

Destination

```
10.10.10.30
```

Commands

```
whoami

hostname

ipconfig
```

Protocol

```
SMB
```

Port

```
445
```

---

# Security Impact

An attacker with valid credentials can:

- Execute arbitrary commands
- Deploy malware
- Dump credentials
- Move laterally
- Install persistence
- Exfiltrate data

---

# Detection

Detected by:

- Sysmon Event ID 1
- Splunk Searches
- Process Creation Monitoring

---

# Recommended Response

1. Disable compromised account

2. Reset credentials

3. Isolate endpoint

4. Collect memory

5. Review authentication history

6. Search for additional lateral movement

---

# Lessons Learned

Remote administrative tools generate identifiable telemetry.

Process creation monitoring provides strong visibility for detecting lateral movement.

---

# Incident Status

Closed