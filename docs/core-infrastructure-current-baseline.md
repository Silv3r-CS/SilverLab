# Core Infrastructure Current Baseline

This document records the current SilverLab infrastructure baseline as of **30 July 2026**, following the physical pfSense migration, VLAN redesign, multi-user Proxmox expansion, remote-access work, and backup implementation.

## Purpose

The purpose of this baseline is to show the current operational foundation of SilverLab and the practical infrastructure skills demonstrated through the build.

## Hardware Roles

| Device | Name | Role |
|---|---|---|
| Laptop 1 | **SILVER-KALI-CLIENT** | Kali administration/security workstation and endpoint/client VM host. |
| Laptop 2 | **SILVER-PVE01** | Proxmox VE infrastructure host with approximately 16 GiB RAM. |
| Fujitsu Futro S720 | **SILVER-FW01** | Dedicated physical pfSense CE firewall. |
| TP-Link TL-SG105E | **SilverLab Managed Switch** | VLAN trunking and access-port switching. |
| TP-Link Archer | **SilverLab Access Point** | Protected LAN wired/wireless access. |
| 1 TB USB drive | **Proxmox Backup Storage** | Scheduled local backup destination. |

## Proxmox Baseline

**SILVER-PVE01** is the central virtualisation host and is managed on VLAN 10 at `10.50.10.200`.

Current or established service roles include:

| System | Role | Notes |
|---|---|---|
| **SILVER-DC01** | Windows Server domain controller | Provides Active Directory and DNS services for `silverlab.local`. |
| **SILVER-WEB01** | Ubuntu/Nginx internal web server | Provides Linux administration and internal service-hosting evidence. |
| Windows client VMs | Domain and support testing | Used for domain join, user support, GPO, DNS, and remote-access scenarios. |

The former pfSense VM is no longer the production firewall. The active firewall role has moved to the physical Fujitsu Futro S720.

## Multi-User Administration

SilverLab has been expanded into a shared learning environment using individual Proxmox accounts.

Implemented and tested areas include:

- Individual student usernames.
- Role-based access control.
- VM creation permissions.
- Storage and ISO access.
- Virtual bridge selection.
- Snapshot and backup permissions.
- Login and password troubleshooting.

This work demonstrates both platform administration and support for other users rather than only single-user homelab operation.

## Current Network Design

| Network | Purpose |
|---|---|
| VLAN 10 | Protected SilverLab LAN using `10.50.10.0/24`. |
| VLAN 99 | WAN transit between the home edge and pfSense. |
| `10.50.20.0/24` | WireGuard remote-access tunnel network. |
| `192.168.50.0/24` | Emergency managed-switch access network. |

Key confirmed addresses:

| Component | Address / role |
|---|---|
| pfSense VLAN 10 gateway | `10.50.10.1` |
| SilverLab access point | `10.50.10.2` |
| SILVER-PVE01 management | `10.50.10.200` |
| TL-SG105E management | `192.168.50.2` |
| pfSense WireGuard interface | `10.50.20.1` |
| First validated WireGuard peer | `10.50.20.2/32` |

The post-migration address for **SILVER-DC01** is intentionally omitted until the updated static-address and DNS configuration has been fully revalidated and documented.

## Managed Switch Design

| Port | Connected device | Configuration |
|---|---|---|
| 1 | Fujitsu Futro S720 | Tagged trunk for VLAN 10 and VLAN 99. |
| 2 | Home edge router | Untagged WAN access on VLAN 99. |
| 3 | SilverLab access point | Untagged protected-LAN access on VLAN 10. |
| 4 | SILVER-PVE01 | Untagged protected-LAN access on VLAN 10. |
| 5 | Emergency management device | Isolated switch-management access. |

The design keeps the home network outside the student-accessible SilverLab environment while allowing pfSense to route and filter traffic for the protected LAN.

## Remote Access Baseline

Two remote-access paths serve different purposes:

| Technology | Purpose |
|---|---|
| Tailscale | Protected access to the Proxmox management interface. |
| WireGuard on pfSense | Access to the SilverLab VLAN 10 network and internal services. |

WireGuard was validated with a remote student client after troubleshooting routing, firewall rules, packet flow, and virtual network-adapter behaviour.

## Windows and Active Directory Progress

- Maintained the `silverlab.local` domain environment.
- Created additional Windows client VMs.
- Joined Windows clients to Active Directory.
- Worked with computer objects and administrative delegation.
- Resolved DNS and local administrator access issues.
- Prepared **SILVER-CLIENT03** for remote domain access through WireGuard.

## Backup Baseline

- Added and mounted a 1 TB USB drive to Proxmox.
- Added the drive as backup storage.
- Created a recurring Proxmox backup job for every Sunday.
- Started the first full scheduled backup run.
- Practised backup and snapshot permission configuration for student users.

A successful backup does not replace restore validation; this baseline records the implemented backup job rather than claiming that a full restore test has already been completed.

## Evidence and Learning Outcomes

- Physical firewall migration from VM to dedicated hardware.
- Router-on-a-stick VLAN design.
- Managed-switch tagged trunk and access-port configuration.
- Protected Proxmox management networking.
- Multi-user Proxmox role and permission administration.
- Active Directory client support and DNS troubleshooting.
- WireGuard peer configuration and remote-access troubleshooting.
- pfSense packet capture and firewall-rule validation.
- USB backup-storage configuration and recurring backup scheduling.
- Physical cabling and network-interface fault diagnosis.

## Portfolio Skills Demonstrated

- Hypervisor and VM administration
- Network segmentation and VLAN implementation
- Managed-switch configuration
- pfSense firewall administration
- WireGuard and Tailscale remote access
- Proxmox role-based access control
- Windows Server and Active Directory support
- DNS, routing, and connectivity troubleshooting
- Packet capture and evidence-based fault finding
- Backup scheduling and storage administration
- Multi-user technical support
- Secure technical documentation
