# SMB Enumeration

## Objective

Enumerate SMB service configuration.

---

## MITRE ATT&CK

T1021.002

---

## Tool

NetExec

---

## Command

```bash
netexec smb 10.10.10.30
```

---

## Information Collected

- Windows Version
- SMB Signing
- SMB Protocol
- Hostname
- Domain

---

## Findings

```
Windows 11
Signing Enabled
SMBv1 Disabled
```

---

## Detection Opportunities

Sysmon

Network Connections

SMB Logs

---

## Security Impact

Enumeration provides attackers with reconnaissance prior to lateral movement.

---

## Conclusion

System information was successfully collected through SMB.