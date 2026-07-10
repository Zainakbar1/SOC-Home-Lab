# File Hashes

## Overview

During a production incident, cryptographic hashes should be collected for all suspicious files prior to removal.

Within this project, no real malware samples were used. Therefore, no malicious file hashes were collected.

---

# Example Commands

```powershell
Get-FileHash payload.exe
```

```powershell
certutil -hashfile payload.exe SHA256
```

---

# Status

No malicious binaries were retained within the repository.