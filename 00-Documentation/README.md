# 📖 SOC Home Lab - Documentation Index

Welcome to the comprehensive documentation for the **SOC Home Lab**. This directory contains step-by-step documentation, command references, configuration details, threat hunting queries, and screenshots for each phase of the attack and defense simulation.

---

## 🗺️ Lab Network Architecture

The environment simulates an enterprise branch network with an attacker workstation, a Windows 11 endpoint, and a central security monitoring server isolated within a virtualized host-only subnet.

```
                           Internet
                               │
                        VMware NAT (VMnet8)
                               │
       ┌────────────────────────┼────────────────────────┐
       │                        │                        │
  Ubuntu-SOC               Windows-SOC               Kali-SOC
192.168.48.137           192.168.48.136           192.168.48.138
 10.10.10.10               10.10.10.30              10.10.10.20
       │                        │                        │
       └────────────────────────┼────────────────────────┘
                   VMware Host-only (VMnet1)
                          10.10.10.0/24
```

---

## 🗂️ Documentation Phases

Navigate to the detailed documentation for each phase using the links below:

### ⚙️ Infrastructure & Network Setup
*   **[Phase 0 – Infrastructure Preparation](Phase0/README.md)**  
    Virtualization setup with VMware Workstation Pro. Creating Ubuntu, Windows 11, and Kali Linux VMs. Hardware allocation, dual network adapters, and baseline snapshot strategy.
*   **[Phase 1 – Network Configuration](Phase1/README.md)**  
    Static IP assignment on the isolated Host-only network (10.10.10.0/24), ping verification, firewall rules for ICMP, and OpenSSH server configuration.

### 📊 Log Collection & Centralization
*   **[Phase 2 – Splunk Enterprise Installation](Phase2/README.md)**  
    Splunk Enterprise deployment on Ubuntu SOC server. Custom index creation (`windows`, `sysmon`, `linux`, `security`) and configuring the receiving port (TCP 9997).
*   **[Phase 3 – Windows Logging & Sysmon](Phase3/README.md)**  
    Splunk Universal Forwarder installation on the Windows endpoint. Sysmon installation with a custom configuration. Configuring `inputs.conf` to forward Event Logs and Sysmon telemetry.
*   **[Phase 5 – Technology Add-ons & Sysmon Parsing](Phase5/README.md)**  
    Splunk Add-ons configuration for Microsoft Windows and Microsoft Sysmon on the Enterprise Server to enable automatic log parsing, field extractions, and CIM compatibility.

### ⚔️ Offensive Simulations
*   **[Phase 4 – Attack Workstation & Reconnaissance](Phase4/README.md)**  
    Attacker machine setup, verifying basic Nmap capabilities. Host discovery sweeps, default port scans, version detection, and OS fingerprinting.
*   **[Phase 6 – Reconnaissance & SMB Enumeration](Phase6/README.md)**  
    Simulating adversary discovery steps. SMB share enumeration, NetBIOS discovery, domain and protocol checking, NetExec credential verification, local administrator check, and PsExec remote shell execution attempt.
*   **[Phase 7 – Threat Hunting & Lateral Movement](Phase7/README.md)**  
    Adversary workflow for credentialed lateral movement. Hydra SMB password sprays, Impacket-psexec authenticated execution, and initial forensic trace collection.

### 🛡️ Defensive Analysis & Operations
*   **[Phase 8 – Incident Response & Threat Hunting](Phase8/README.md)**  
    Post-compromise investigation following the NIST Incident Response Lifecycle. Splunk SPL searches to identify persistence (registry run keys, scheduled tasks), reconstruct the attack timeline, identify indicators of compromise (IOCs), and map to MITRE ATT&CK.
*   **[Phase 9 – Portfolio Documentation & Finalization](Phase9/README.md)**  
    Reviewing repository organization, validating detection rules, collecting incident reports, preparing resume descriptions, and finalizing the portfolio.
    *   *Sub-documents:* [Architecture](Phase9/Architecture.md) | [Installation](Phase9/Installation.md) | [Lessons Learned](Phase9/LessonsLearned.md) | [Network](Phase9/Network.md) | [Screenshots](Phase9/Screenshots.md) | [Troubleshooting](Phase9/Troubleshooting.md)
*   **[Phase 10 – Lessons Learned & Incident Reports](../07-Incident-Reports/LessonsLearned/README.md)**  
    Final incident response lifecycle summary, post-incident reviews, containment and recovery steps, and future improvement plans.

---

## 🛠️ Lab Specifications & Inventory

| Machine | IP Address | OS | Installed Core Components |
|:---|:---|:---|:---|
| **Ubuntu-SOC** | 10.10.10.10 | Ubuntu 24.04 / 26.04 | Splunk Enterprise (Indexer/Web), OpenSSH Server |
| **Kali-SOC** | 10.10.10.20 | Kali Linux | Nmap, NetExec, Impacket, Hydra, Metasploit |
| **Windows-SOC** | 10.10.10.30 | Windows 11 Pro | Splunk Universal Forwarder, Microsoft Sysmon v15 |
