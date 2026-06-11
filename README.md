# SilverLab Homelab

SilverLab is my personal IT homelab project built to develop practical, job-ready skills in virtualization, networking, Linux administration, troubleshooting, documentation, and infrastructure planning.

The lab uses a repurposed laptop running Proxmox VE as the virtualization host, with a separate admin workstation used for browser access, SSH, documentation, and future lab management tasks.

This repository documents the build process, design decisions, troubleshooting steps, and future improvements.

## Project Goals

The purpose of this homelab is to build hands-on experience that supports a career in IT support, systems administration, networking, and cybersecurity.

Key goals include:

- Build and manage a Proxmox VE virtualization host
- Create and manage Linux and Windows virtual machines
- Practice network troubleshooting and documentation
- Build a small lab network separate from normal home usage
- Learn Active Directory, DNS, DHCP, monitoring, backups, and security basics
- Document the project professionally as portfolio evidence

## Current Lab Status

The second infrastructure phase of the lab is complete.

Current progress:

- Proxmox VE installed on Laptop 2
- Proxmox accessible from Laptop 1 through a browser
- Built-in LAN adapter on Laptop 2 identified as faulty and left unused
- USB-to-LAN adapter installed and confirmed working
- Proxmox bridge `vmbr0` configured to use the USB-to-LAN adapter
- Original Technicolor router replaced with a TP-Link Archer C6
- New lab Wi-Fi network created: **SilverHomeLab**
- Lab network migrated to the `192.168.1.x` subnet
- Proxmox management IP updated to `192.168.1.200/24`
- Tailscale secure remote access to Proxmox confirmed
- First Ubuntu Server VM installed and baselined
- SSH access to the Ubuntu Server VM confirmed from Laptop 1
- QEMU Guest Agent installed and validated inside the Ubuntu Server VM
- Baseline snapshot created after SSH and QEMU Guest Agent validation

## Contribution History

| Contribution | Summary | Documentation |
|---|---|---|
| 01 | Initial Proxmox installation, lab network setup, USB-to-LAN adapter fix, and first topology documentation | `docs/01-initial-lab-build.md`, `docs/02-troubleshooting-usb-lan-fix.md` |
| 02 | TP-Link Archer C6 migration, subnet migration, Tailscale recovery, Ubuntu Server baseline, SSH validation, QEMU Guest Agent validation, and baseline snapshot | `docs/03-ubuntu-server-baseline.md`, `docs/04-archer-c6-router-migration.md` |

## Current Network Topology

```text
Home Router / Main Internet
        |
Mini Switch
        |
TP-Link Archer C6
SilverHomeLab Wi-Fi / Lab Network
Gateway: 192.168.1.1
        |
USB-to-LAN Adapter
        |
Laptop 2 - Proxmox VE Host
IP: 192.168.1.200/24
        |
vmbr0 Bridge
        |
Ubuntu Server VM
Future Virtual Machines
```

A Mermaid version of the current topology is stored in:

```text
assets/diagrams/current-topology.mmd
```

## Proxmox Network Configuration

The working Proxmox network configuration uses `vmbr0` as the management and VM bridge.

```text
auto lo
iface lo inet loopback

iface nic1 inet manual

auto vmbr0
iface vmbr0 inet static
        address 192.168.1.200/24
        gateway 192.168.1.1
        bridge-ports nic1
        bridge-stp off
        bridge-fd 0

iface nic0 inet manual

iface nic2 inet manual

source /etc/network/interfaces.d/*
```

## Interface Summary

| Interface | Purpose | Status |
|---|---|---|
| `nic0` | Built-in LAN adapter | Faulty / unused |
| `nic1` | USB-to-LAN adapter | Active |
| `wlo1` | Built-in Wi-Fi adapter | Not used by Proxmox |
| `vmbr0` | Proxmox Linux bridge | Active, `192.168.1.200/24` |

## Storage Summary

The Proxmox host has a 256 GB SSD. Linux reports this as approximately 238.5 GiB usable.

Current layout:

| Storage Area | Approximate Size | Purpose |
|---|---:|---|
| Proxmox root | 69.5 GiB | Host operating system |
| local-lvm / data | 141.5 GiB | VM disks |
| Swap | 7.6 GiB | System swap |

The Proxmox dashboard displays the root filesystem size, not the entire SSD. The remaining storage is available for virtual machine disks through `local-lvm`.

## First Ubuntu Server VM

The first Ubuntu Server VM has been installed and baselined.

| Setting | Value |
|---|---|
| VM name | `SilverServer-Ubuntu` |
| Hostname | `homelab-silver` |
| CPU | 2 cores |
| RAM | 2 GiB |
| Disk | 32 GiB on `local-lvm` |
| Network | VirtIO adapter on `vmbr0` |
| SSH | Enabled and tested from Laptop 1 |
| QEMU Guest Agent | Installed and validated |
| Snapshot | `ubuntu-baseline-ssh-qemu-agent-working` |

## Secure Remote Access

SilverLab uses Tailscale for secure remote access to Proxmox.

This avoids exposing the Proxmox web interface directly to the public internet and removes the need for public port forwarding.

## Skills Demonstrated

This project currently demonstrates:

- Installing and accessing Proxmox VE
- Reading Linux network interface output
- Identifying a faulty network adapter
- Replacing a failed internal LAN interface with a USB-to-LAN adapter
- Configuring a Proxmox Linux bridge
- Assigning and updating a static management IP
- Replacing and configuring a lab router
- Migrating a lab subnet
- Recovering Proxmox access after a gateway/subnet change
- Validating secure remote access using Tailscale
- Installing and baselining an Ubuntu Server VM
- Using SSH for remote Linux administration
- Installing and validating QEMU Guest Agent
- Creating a baseline VM snapshot
- Documenting infrastructure in a professional format

## Next Steps

The next milestones are:

- Add DHCP/address reservations on the TP-Link Archer C6
- Reserve the Proxmox management address
- Reserve or document the Ubuntu Server VM address
- Continue building the next SilverLab service layer
- Add monitoring/SIEM practice using dedicated lab endpoints
- Plan OPNsense deployment after a second USB-to-LAN adapter is available

## Planned Future Work

Future phases of the lab will include:

- Additional Linux administration VMs
- Windows Server VM
- Active Directory, DNS, and DHCP practice
- Windows client VM for domain-join testing
- Monitoring and logging with Splunk and/or Wazuh
- Backup and restore testing
- OPNsense firewall and network segmentation
- Secure file services using external storage
- Documentation updates for each major milestone
