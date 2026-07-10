# Indicators of Compromise (IOCs)

## Host Indicators

- Windows-SOC
- 10.10.10.30

---

## Network Indicators

- TCP 445 (SMB)
- TCP 9997 (Splunk Forwarder)

---

## Process Indicators

- PSEXESVC
- cmd.exe
- powershell.exe
- net.exe
- schtasks.exe

---

## Registry Indicators

HKLM\Software\Microsoft\Windows\CurrentVersion\Run

HKCU\Software\Microsoft\Windows\CurrentVersion\Run

---

## Event IDs

- Sysmon 1
- Sysmon 3
- Sysmon 11
- Sysmon 12
- Sysmon 13
- Windows 4624
- Windows 4625
- Windows 5140