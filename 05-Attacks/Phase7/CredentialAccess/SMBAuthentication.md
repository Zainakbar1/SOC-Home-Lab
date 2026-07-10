# SMB Authentication Attack

## Objective

The objective of this exercise was to validate SMB authentication against the Windows target using known administrative credentials. This demonstrates how attackers leverage valid credentials to authenticate to remote systems without exploiting software vulnerabilities.

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Valid Accounts | T1078 |
| SMB/Windows Admin Shares | T1021.002 |

---

## Target

| Host | IP |
|------|----|
| Windows-SOC | 10.10.10.30 |

Attacker:

| Host | IP |
|------|----|
| Kali-SOC | 10.10.10.20 |

---

## Tool Used

- NetExec
- smbclient

---

## Command Used

```bash
netexec smb 10.10.10.30 -u socadmin -p root
```

---

## Result

Authentication succeeded.

Output confirmed:

- SMB service reachable
- Valid credentials
- Administrative privileges
- Pwn3d status

Example:

```
[+] WINDOWS-SOC\socadmin:root (Pwn3d!)
```

---

## Security Impact

An attacker possessing valid credentials can:

- Access SMB shares
- Enumerate the system
- Execute remote commands
- Move laterally inside the network

---

## Detection Opportunities

- Windows Security Event ID 4624
- Sysmon Process Creation
- SMB Session Monitoring
- Netlogon events

---

## MITRE Mapping

- T1078
- T1021.002

---

## Conclusion

Successful SMB authentication confirmed that administrative credentials were valid and could be used for lateral movement.