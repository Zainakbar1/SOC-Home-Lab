# Reconnaissance

## ATT&CK Tactic

Reconnaissance

---

# Techniques

## T1018 - Remote System Discovery

### Description

Identify active hosts on the target network.

### Activity

- ICMP Ping
- Host Discovery

### Tools

- Nmap

### Commands

```bash
ping 10.10.10.30
sudo nmap -sn 10.10.10.0/24
```

### Detection

```spl
index=sysmon EventCode=3
```

---

## T1046 - Network Service Discovery

### Description

Identify open network services.

### Activity

- SYN Scan
- Service Detection
- Aggressive Scan

### Commands

```bash
sudo nmap -sS 10.10.10.30
sudo nmap -sV 10.10.10.30
sudo nmap -A 10.10.10.30
```

### Detection

```spl
index=sysmon EventCode=3
```

---

## Phase

Phase 6