# SilverLab Homelab

SilverLab is my personal IT homelab project built to develop practical, job-ready skills in virtualization, networking, Linux administration, troubleshooting, documentation, and infrastructure planning.

The lab currently uses a repurposed laptop running Proxmox VE as the virtualization host. A separate lab Wi-Fi network named **SilverLab** has been created using a reconfigured Technicolor TG582n router.

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

The first physical phase of the lab is complete.

Current progress:

- Proxmox VE installed on Laptop 2
- Proxmox accessible from Laptop 1 through a browser
- Built-in LAN adapter on Laptop 2 identified as faulty
- USB-to-LAN adapter installed and confirmed working
- Proxmox bridge `vmbr0` configured to use the USB-to-LAN adapter
- Technicolor TG582n router reconfigured for the lab
- New lab Wi-Fi network created: **SilverLab**
- Proxmox management IP configured as `192.168.0.200/24`

## Current Network Topology

```text
Home Router / Main Internet
        |
Technicolor TG582n
SilverLab Wi-Fi / Lab Network
        |
USB-to-LAN Adapter
        |
Laptop 2 - Proxmox VE Host
IP: 192.168.0.200/24
        |
Future Virtual Machines
```

## Proxmox Network Configuration

The working Proxmox network configuration uses `vmbr0` as the management and VM bridge.

```text
auto lo
iface lo inet loopback

iface nic1 inet manual

auto vmbr0
iface vmbr0 inet static
        address 192.168.0.200/24
        gateway 192.168.0.1
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
| `vmbr0` | Proxmox Linux bridge | Active, `192.168.0.200/24` |

## Storage Summary

The Proxmox host has a 256 GB SSD. Linux reports this as approximately 238.5 GiB usable.

Current layout:

| Storage Area | Approximate Size | Purpose |
|---|---:|---|
| Proxmox root | 69.5 GiB | Host operating system |
| local-lvm / data | 141.5 GiB | VM disks |
| Swap | 7.6 GiB | System swap |

The Proxmox dashboard displays the root filesystem size, not the entire SSD. The remaining storage is available for virtual machine disks through `local-lvm`.

## Skills Demonstrated

This first stage demonstrates:

- Installing and accessing Proxmox VE
- Reading Linux network interface output
- Identifying a faulty network adapter
- Replacing a failed internal LAN interface with a USB-to-LAN adapter
- Configuring a Proxmox Linux bridge
- Assigning a static management IP
- Reconfiguring a router for lab use
- Creating a separate lab Wi-Fi network
- Documenting infrastructure in a professional format

## Next Steps

The next milestone is to create the first virtual machine:

```text
VM name: ubuntu-admin-01
OS: Ubuntu Server
CPU: 2 cores
RAM: 2 GB
Disk: 20 GB
Storage: local-lvm
Network: vmbr0
```

After installation, the VM will be tested for:

- IP address assignment
- Gateway connectivity
- Internet access
- DNS resolution
- Access from Laptop 1
- SSH access

## Planned Future Work

Future phases of the lab will include:

- Ubuntu administration VM
- Windows Server VM
- Active Directory domain controller
- DNS and DHCP services
- File sharing
- Monitoring and logging
- Backup and restore testing
- Security testing VM
- Network diagrams and screenshots
- Lessons learned documentation

## Repository Structure

```text
silverlab-homelab/
├── README.md
├── docs/
│   ├── 01-initial-lab-build.md
│   └── 02-troubleshooting-usb-lan-fix.md
└── assets/
    └── diagrams/
        └── current-topology.mmd
```

## Notes

This repository intentionally avoids uploading passwords, private keys, public IP addresses, serial numbers, VM disk files, ISO files, and other sensitive data.
