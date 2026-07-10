# Incident Report IR-004

# Complete Attack Timeline

---

## Objective

Reconstruct the complete attacker activity from reconnaissance to remote execution.

---

## Timeline

### Phase 1

Network Discovery

```
Ping Sweep
```

---

### Phase 2

Host Discovery

```
Nmap Scan
```

---

### Phase 3

Service Enumeration

```
Version Detection

OS Detection

Aggressive Scan
```

---

### Phase 4

SMB Enumeration

```
SMB Version

Signing

Security Mode

Shares
```

---

### Phase 5

Authentication

```
NetExec Authentication

smbclient Authentication
```

---

### Phase 6

Privilege Validation

```
Pwn3d

Administrative Shares
```

---

### Phase 7

Remote Execution

```
Impacket PsExec
```

---

### Phase 8

Command Execution

```
whoami

hostname

ipconfig
```

---

### Phase 9

Detection

```
Sysmon

Splunk

Threat Hunting
```

---

## ATT&CK Chain

Reconnaissance

↓

Discovery

↓

Credential Access

↓

Lateral Movement

↓

Execution

↓

Detection

---

## Findings

The simulated attack successfully demonstrated the complete attack lifecycle.

Each phase generated telemetry suitable for detection and investigation.

---

## Conclusion

The SOC successfully detected attacker activity throughout the attack lifecycle.