# Discovery

## T1135 - Network Share Discovery

### Activity

SMB Enumeration

### Tools

- Nmap
- NetExec

### Commands

```bash
sudo nmap --script smb-enum-shares 10.10.10.30

netexec smb 10.10.10.30 -u socadmin -p root --shares
```

### Detection

```spl
index=sysmon DestinationPort=445
```

---

## Phase

Phase 6