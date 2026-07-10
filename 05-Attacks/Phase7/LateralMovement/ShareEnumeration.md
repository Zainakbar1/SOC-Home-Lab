# SMB Share Enumeration

## Objective

Enumerate available SMB shares after successful authentication.

---

## Command

```bash
netexec smb 10.10.10.30 -u socadmin -p root --shares
```

---

## Shares Found

- ADMIN$
- C$
- IPC$

---

## Permissions

ADMIN$

Read

Write

C$

Read

Write

IPC$

Read

---

## Security Impact

Administrative shares allow attackers to:

- Upload malware
- Execute payloads
- Copy tools
- Move laterally

---

## Detection

Monitor:

- SMB Share Access

- File Upload Activity

- Administrative Share Access

---

## MITRE

T1021.002

---

## Conclusion

Authenticated enumeration revealed writable administrative shares.