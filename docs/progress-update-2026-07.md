# SilverLab Progress Update - July 2026

This update records practical progress completed after the previous GitHub milestone on **19 June 2026**.

## Progress Summary

SilverLab has developed from a single-host virtualisation and Active Directory lab into a more structured, multi-user environment with a dedicated physical firewall, managed VLAN network, remote student access, and scheduled backup storage.

## Physical Firewall and Network Segmentation

- Migrated the active pfSense firewall from a Proxmox VM to a dedicated Fujitsu Futro S720.
- Implemented a one-NIC router-on-a-stick design.
- Configured VLAN 10 as the protected SilverLab LAN using `10.50.10.0/24`.
- Configured VLAN 99 as the WAN transit network.
- Configured a TP-Link TL-SG105E managed switch with tagged trunking and untagged access ports.
- Moved Proxmox management to VLAN 10 at `10.50.10.200`.
- Connected the SilverLab access point to VLAN 10 at `10.50.10.2`.
- Maintained separation between the home network and student-accessible lab systems.

## Proxmox Multi-User Environment

- Expanded the Proxmox host to approximately 16 GiB RAM.
- Created individual student accounts.
- Configured and troubleshot role-based permissions.
- Enabled practical access to VM creation, storage, ISO images, network bridges, snapshots, and backups.
- Resolved login, password, storage-selection, bridge-selection, and snapshot-deletion issues.
- Began evaluating Proxmox Datacenter Manager for future external-node visibility and centralised learning.

## Windows Server and Active Directory

- Continued operating the `silverlab.local` Active Directory environment.
- Created additional Windows client VMs.
- Joined Windows clients to the domain.
- Worked with computer accounts, administrative access, and delegated permissions.
- Resolved DNS, domain connectivity, and missing local administrator issues.
- Prepared **SILVER-CLIENT03** for remote Active Directory access.

## WireGuard Remote Access

- Configured WireGuard on pfSense.
- Created the `10.50.20.0/24` tunnel network.
- Assigned pfSense the tunnel address `10.50.20.1`.
- Created an individual remote peer using `10.50.20.2/32`.
- Configured access to the protected `10.50.10.0/24` network.
- Used pfSense firewall rules, packet capture, tunnel status, routing checks, and client adapter troubleshooting.
- Successfully established the first remote student connection.

Tailscale remains the protected remote-management path for Proxmox access, while WireGuard provides access to internal SilverLab network services.

## Backup Implementation

- Added a 1 TB USB drive to the Proxmox host.
- Mounted and added the drive as Proxmox backup storage.
- Created a recurring backup job scheduled for every Sunday.
- Started the first full backup run.
- Practised backup and snapshot permission administration for multi-user access.

This milestone records backup implementation. Restore testing will only be documented as completed after a backup has been successfully restored and validated.

## Troubleshooting and Operational Learning

- Diagnosed physical Ethernet cabling faults and link-speed problems.
- Investigated USB network-adapter behaviour.
- Used pfSense packet capture to diagnose VPN traffic.
- Resolved Windows DNS and domain-join issues.
- Recovered access where no known local Windows administrator was available.
- Configured Proxmox permissions using practical student support scenarios.
- Used Jira-style planning for infrastructure, SQL, cybersecurity, and AI-assisted documentation projects.

## Updated Topology

```mermaid
flowchart LR
    Internet((Internet)) --> HomeRouter[Home Edge Router]
    HomeRouter -->|VLAN 99 WAN transit| Switch[TP-Link TL-SG105E]
    Switch -->|Tagged VLAN 99 + VLAN 10 trunk| FW[SILVER-FW01\nPhysical pfSense]
    FW -->|VLAN 10\n10.50.10.1/24| Switch

    Switch -->|VLAN 10| PVE[SILVER-PVE01\nProxmox VE\n10.50.10.200]
    Switch -->|VLAN 10| AP[SilverLab Access Point\n10.50.10.2]

    PVE --> DC[SILVER-DC01\nActive Directory and DNS]
    PVE --> WEB[SILVER-WEB01\nUbuntu and Nginx]
    PVE --> Clients[Windows Client VMs]
    USB[(1 TB USB Backup Storage)] --> PVE

    RemoteStudent[Remote Student Device] -. WireGuard 10.50.20.0/24 .-> FW
    RemoteUser[Remote Proxmox User] -. Tailscale .-> PVE
```

## Skills Demonstrated

- Proxmox VE administration
- Virtual machine and storage management
- Role-based access control
- Multi-user technical support
- pfSense firewall deployment
- Router-on-a-stick networking
- VLAN design and managed-switch configuration
- Network segmentation
- WireGuard and Tailscale remote access
- Active Directory and Windows client support
- DNS, routing, and firewall troubleshooting
- Packet capture and structured fault finding
- Backup scheduling and storage administration
- Technical documentation and change tracking
