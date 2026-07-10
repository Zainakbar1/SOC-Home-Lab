# Eradication Verification

## Overview

Following artifact removal, verification activities were performed to ensure the Windows endpoint no longer contained indicators of compromise associated with the simulated attack.

---

# Verification Checklist

- PsExec service removed
- Registry persistence removed
- Scheduled tasks removed
- Temporary payloads removed
- SMB sessions terminated
- No suspicious processes
- No unauthorized users
- No unauthorized services

---

# Verification Commands

```powershell
Get-Service PSEXESVC
```

```powershell
Get-ScheduledTask
```

```powershell
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
```

```powershell
Get-LocalUser
```

---

# Evidence

- Splunk Searches
- Sysmon Events
- Windows Security Logs
- Registry Review

---

# Outcome

Verification confirmed successful eradication of all simulated attack artifacts. The endpoint was considered ready for recovery.