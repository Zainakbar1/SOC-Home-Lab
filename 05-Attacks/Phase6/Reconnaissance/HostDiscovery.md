# Host Discovery

## Overview

Host Discovery was the first reconnaissance activity performed during Phase 6 of the SOC Home Lab. The objective was to verify that the target Windows endpoint was reachable from the Kali attack workstation before performing additional enumeration.

This activity simulates the initial network reconnaissance commonly performed by attackers after gaining access to a network.

---

# Objective

- Verify network connectivity
- Identify live hosts
- Validate lab network configuration
- Generate telemetry for detection validation

---

# Environment

| Component | Value |
|-----------|-------|
| Attacker | Kali-SOC |
| Target | Windows-SOC |
| Attacker IP | 10.10.10.20 |
| Target IP | 10.10.10.30 |
| Network | 10.10.10.0/24 |

---

# MITRE ATT&CK

| Tactic | Technique |
|--------|-----------|
| Discovery | T1016 – System Network Configuration Discovery |
| Discovery | T1046 – Network Service Discovery |

---

# Commands Executed

### ICMP Ping

```bash
ping -c 4 10.10.10.30
```

### Nmap Host Discovery

```bash
nmap -sn 10.10.10.30
```

---

# Expected Result

- Target responds to ICMP requests
- Host identified as online
- Network connectivity confirmed

---

# Actual Result

The Windows endpoint successfully responded to host discovery requests. Network connectivity between Kali-SOC and Windows-SOC was confirmed, allowing subsequent reconnaissance and attack simulation activities.

---

# Detection Opportunities

This activity may generate telemetry useful for:

- Network reconnaissance monitoring
- ICMP activity analysis
- Nmap detection
- Host discovery alerts

---

# Evidence

Related screenshots:

- Phase7-01 – Nmap Service Verification
- Phase7-02 – SSH Port Check

---

# Outcome

Host discovery successfully confirmed connectivity between the attacker and target systems. This established the foundation for subsequent port scanning, service enumeration, and SMB-based attack simulations performed during Phase 6.