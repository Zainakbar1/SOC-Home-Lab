Architecture
                 INTERNET
                     │
             VMware NAT Network
                     │
      ┌──────────────┼───────────────┐
      │              │               │
      │              │               │
 Ubuntu SOC      Kali Linux      Windows 11
 10.10.10.10     10.10.10.20      10.10.10.30
      │              │               │
      └────── Host Only SOC Network ─┘

Ubuntu
--------
Splunk Enterprise
SSH Server
Syslog Server
Universal Forwarder Management

Windows
---------
Sysmon
Splunk Universal Forwarder

Kali
-------
Nmap
Metasploit
Burp Suite
Hydra
Gobuster
Impacket
Project Folder Structure
SOC-LAB/

│
├── 00-Documentation
│   ├── README.md
│   ├── Network_Diagram.drawio
│   ├── IP_Addressing.xlsx
│   ├── Screenshots
│   │
│   ├── Phase0
│   ├── Phase1
│   ├── Phase2
│   └── Phase3
│
├── 01-ISO
│   ├── ubuntu-26.04.iso
│   ├── kali-linux.iso
│   ├── windows11.iso
│   └── VMwareTools
│
├── 02-VMs
│   ├── Ubuntu-SOC
│   ├── Kali
│   └── Windows11
│
├── 03-Splunk
│   ├── Enterprise
│   ├── Apps
│   ├── Forwarders
│   ├── Configurations
│   └── Dashboards
│
├── 04-Sysmon
│
├── 05-Attacks
│
├── 06-Detections
│
├── 07-Incident-Reports
│
├── 08-PCAP
│
├── 09-Tools
│
└── Snapshots
Phase Roadmap

We won't rush.

Phase 0
──────────────
✔ VMware Installation
✔ Download ISOs
✔ Create VM Folder Structure
✔ Create Networks
✔ Create Ubuntu VM

Phase 1
──────────────
Ubuntu Installation
Networking
SSH
Updates
Snapshots

Phase 2
──────────────
Install Splunk
Create Indexes
Create Users
Receive Logs

Phase 3
──────────────
Windows Installation
Sysmon
Forwarder

Phase 4
──────────────
Kali Installation

Phase 5
──────────────
Attack Simulation

Phase 6
──────────────
Detection Engineering

Phase 7
──────────────
Threat Hunting

Phase 8
──────────────
Incident Response

Phase 9
──────────────
Portfolio Documentation
VMware VM Specifications
Ubuntu (SOC Server)
Setting	Value
Name	Ubuntu-SOC
Compatibility	Latest VMware Version
Guest OS	Ubuntu 64-bit
Firmware	UEFI
CPU	4 vCPU
RAM	12 GB
Disk	80 GB NVMe
Network Adapter 1	NAT
Network Adapter 2	Host Only
USB	USB 3.1
Sound	Disabled
Printer	Disabled
Kali
Setting	Value
CPU	4 vCPU
RAM	8 GB
Disk	40 GB
Adapter 1	NAT
Adapter 2	Host Only
Windows 11
Setting	Value
CPU	4 vCPU
RAM	8 GB
Disk	80 GB
Adapter 1	NAT
Adapter 2	Host Only

Total RAM allocated while all VMs are running: 28 GB, leaving about 12 GB for your Windows host, which is a comfortable balance.

Network Plan
Machine	NAT	SOC Network
Ubuntu	DHCP	10.10.10.10/24
Kali	DHCP	10.10.10.20/24
Windows	DHCP	10.10.10.30/24

Host-only network:

10.10.10.0/24

Gateway:

None

DNS:

None

This isolated network keeps attack traffic contained within the lab.

Snapshot Strategy

We'll create a VMware snapshot after every major milestone:

Snapshot 01
Fresh Install

Snapshot 02
Ubuntu Updated

Snapshot 03
Splunk Installed

Snapshot 04
Windows Installed

Snapshot 05
Sysmon Configured

Snapshot 06
Kali Ready

Snapshot 07
Complete Lab
Documentation Standards

For every phase, we'll produce:

Detailed README
Terminal commands
Explanations of each step
Network diagrams
Troubleshooting notes
Commands used
Required screenshots
Portfolio-ready documentation

I'll also tell you exactly when to take screenshots so your documentation is complete.