# Phase 0 – Infrastructure Preparation

## Objective

The objective of this phase was to prepare the virtualization infrastructure for the SOC Home Lab. This included creating the required virtual machines, allocating hardware resources, configuring the VMware virtual networks, and establishing clean baseline snapshots before deploying SOC components.

---

## Lab Environment

| Component | Specification |
|-----------|---------------|
| Host OS | Windows 11 |
| Hypervisor | VMware Workstation Pro |
| CPU | AMD Ryzen 7 7480HS |
| RAM | 40 GB DDR5 |
| GPU | NVIDIA RTX 4050 Laptop GPU (6 GB VRAM) |
| Storage | 512 GB NVMe SSD |

---

📷 **Screenshot Placeholder**  
> VMware Workstation Library (../Screenshots/Phase0/00 - vmware-library.png)

*Figure 1: VMware Workstation Pro displaying the virtual machines created for the SOC Home Lab.*

---

# Virtual Machines

## Ubuntu-SOC

**Purpose**

- Splunk Enterprise Server
- Centralized Log Collection

| Resource | Value |
|----------|-------|
| Operating System | Ubuntu 24.04.2 LTS Desktop |
| CPU | 4 vCPU |
| RAM | 12 GB |
| Disk | 80 GB |
| Network | NAT + Host-only |

📷 **Screenshot Placeholder**  
> Ubuntu VM Settings (../Screenshots/Phase0/01 - ubuntu-vm-settings.png)

*Figure 2: VMware Workstation configuration for the Ubuntu-SOC virtual machine.*

---

## Windows-SOC

**Purpose**

- Endpoint Machine
- Sysmon
- Splunk Universal Forwarder

| Resource | Value |
|----------|-------|
| Operating System | Windows 11 Pro |
| CPU | 4 vCPU |
| RAM | 8 GB |
| Disk | 64 GB |
| Network | NAT + Host-only |

📷 **Screenshot Placeholder**  
> Windows VM Settings (../Screenshots/Phase0/02 - windows-vm-settings.png)

*Figure 3: VMware Workstation configuration for the Windows-SOC virtual machine.*

---

## Kali-SOC

**Purpose**

- Attack Simulation
- Penetration Testing
- Security Assessment

| Resource | Value |
|----------|-------|
| Operating System | Kali Linux |
| CPU | 4 vCPU |
| RAM | 8 GB |
| Disk | 40 GB |
| Network | NAT + Host-only |

📷 **Screenshot Placeholder**  
> Kali VM Settings (../Screenshots/Phase0/03 - kali-vm-settings.png)

*Figure 4: VMware Workstation configuration for the Kali-SOC virtual machine.*

---

# VMware Network Configuration

Two virtual network adapters were configured for each virtual machine:

- **VMnet8 (NAT):** Provides Internet connectivity for updates and software downloads.
- **VMnet1 (Host-only):** Reserved for isolated communication between the lab virtual machines.

> [!NOTE]
> The Host-only network has been created using the **10.10.10.0/24** subnet. Static IP addresses will be assigned during **Phase 1 – Network Configuration**.

### Planned IP Addressing

| Virtual Machine | Planned IP Address |
|-----------------|--------------------|
| Ubuntu-SOC | 10.10.10.10/24 |
| Kali-SOC | 10.10.10.20/24 |
| Windows-SOC | 10.10.10.30/24 |

📷 **Screenshot Placeholder**  
> VMware Virtual Network Editor (../Screenshots/Phase0/04 - vmware-virtual-network-editor.png)

*Figure 5: VMware Virtual Network Editor configured with VMnet1 (Host-only) using the 10.10.10.0/24 subnet and VMnet8 (NAT) for Internet connectivity.*

---

# VMware Snapshots

Baseline snapshots were created after completing each operating system installation.

| Virtual Machine | Snapshot Name |
|-----------------|---------------|
| Ubuntu-SOC | Snapshot 01 – Ubuntu Base Installation |
| Windows-SOC | Snapshot 02 – Windows Base Installation |
| Kali-SOC | Snapshot 03 – Kali Base Installation |

---

# Tasks Completed

- ✅ Installed VMware Workstation Pro
- ✅ Created the Ubuntu-SOC virtual machine
- ✅ Installed Ubuntu 24.04.2 LTS Desktop
- ✅ Created the Windows-SOC virtual machine
- ✅ Installed Windows 11 Pro
- ✅ Created the Kali-SOC virtual machine
- ✅ Installed Kali Linux
- ✅ Installed VMware Tools / Open VM Tools
- ✅ Configured VMware virtual networks (NAT and Host-only)
- ✅ Added dual network adapters to all virtual machines
- ✅ Created baseline snapshots for all virtual machines

---

# Verification

The following components were successfully verified:

- ✅ Ubuntu booted successfully
- ✅ Windows booted successfully
- ✅ Kali booted successfully
- ✅ VMware Tools / Open VM Tools operational
- ✅ NAT network functioning correctly
- ✅ Host-only network (VMnet1) created
- ✅ Virtual machines ready for further configuration

---

# Result

Phase 0 successfully established the virtual infrastructure for the SOC Home Lab. Ubuntu, Windows, and Kali virtual machines were deployed, VMware networking was prepared, and baseline snapshots were created. The environment is now ready for network configuration, static IP assignment, and deployment of SOC components.

---

# Next Phase

## Phase 1 – Network Configuration

In the next phase, the following tasks will be completed:

- Configure static IP addresses
- Configure the Host-only network on all virtual machines
- Verify connectivity between Ubuntu, Windows, and Kali
- Configure OpenSSH on Ubuntu
- Prepare the Ubuntu server for Splunk Enterprise installation