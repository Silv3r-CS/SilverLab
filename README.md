# SilverLab

SilverLab is a practical IT and cyber security homelab built to develop and demonstrate infrastructure, networking, Linux, Windows Server, security, documentation, and troubleshooting skills.

The lab is built on repurposed laptop hardware using Proxmox VE, Ubuntu Server, Windows Server, Tailscale, and a dedicated lab router. The long-term goal is to evolve the environment into a segmented security lab with OPNsense, Active Directory, monitoring, backups, and documented incident-style troubleshooting.

## Current Status

| Area | Status |
|---|---|
| Proxmox VE host | Built and operational on Laptop 2 |
| Lab router | TP-Link Archer C6 configured on `192.168.1.0/24` |
| Ubuntu Server VM | Built, baselined, reachable by SSH |
| Ubuntu Nginx service | Custom internal web page deployed |
| Ubuntu firewall | UFW enabled with SSH and HTTP allowed |
| Tailscale | Secure remote access evidence documented |
| Windows Server VM | Installed, renamed, network validated, RDP working |
| Active Directory | Next milestone |
| OPNsense segmentation | Planned later milestone |
| Monitoring/SIEM | Planned later milestone |
| Backup/restore testing | Planned later milestone |

## Hardware Overview

| Device | Role |
|---|---|
| Laptop 1 | Admin workstation for Proxmox access, SSH, RDP, GitHub documentation, screenshots, and future client/security workloads |
| Laptop 2 | Proxmox VE host with 8 GiB RAM |
| TP-Link Archer C6 | Dedicated lab router and DHCP gateway |
| USB-to-LAN adapter | Working network interface for Proxmox bridge after built-in RJ45 issues |
| External SilverStore drive | Future backup, ISO/archive, and restore-testing storage |

## Current Network Overview

| Component | Address / Role |
|---|---|
| Lab gateway | `192.168.1.1` |
| DHCP pool | `192.168.1.100 - 192.168.1.199` |
| Proxmox host | `192.168.1.200` |
| Ubuntu Server | `192.168.1.120` |
| Windows Server | `192.168.1.154` |
| Proxmox bridge | `vmbr0` using the working USB-to-LAN adapter |

Private lab IP addresses are documented because they describe the internal lab design. Public IPs, passwords, tokens, private keys, MAC addresses, and personal details are excluded or redacted.

## Implemented Milestones

### 1. Proxmox and Network Foundation

- Installed Proxmox VE on Laptop 2
- Identified and worked around the defective built-in RJ45 path
- Configured Proxmox networking through the working USB-to-LAN adapter
- Documented `vmbr0`, storage layout, and baseline host configuration

Documentation:

- [Network Topology](docs/02-network-topology.md)
- [Proxmox Installation and Networking](docs/03-proxmox-installation-and-networking.md)
- [Fault Finding: Laptop 2 RJ45](docs/04-fault-finding-laptop2-rj45.md)

### 2. Router Replacement and Subnet Migration

- Replaced the earlier router setup with a TP-Link Archer C6
- Migrated the lab from the old `192.168.0.x` range to `192.168.1.x`
- Restored Proxmox access after the subnet change
- Confirmed Ubuntu and Proxmox connectivity to the new gateway

Documentation:

- [Router Replacement and Subnet Migration](docs/05-router-replacement-and-subnet-migration.md)

### 3. Ubuntu Server Baseline

- Built an Ubuntu Server VM
- Configured SSH access
- Installed baseline admin tools
- Validated network settings, storage, memory, uptime, and QEMU Guest Agent

Documentation:

- [Ubuntu Server Baseline](docs/06-ubuntu-server-baseline.md)

### 4. Secure Remote Access

- Used Tailscale for secure remote access
- Avoided public Proxmox exposure and public port forwarding
- Documented remote-access security rationale

Documentation:

- [Secure Remote Access with Tailscale](docs/07-secure-remote-access-tailscale.md)

### 5. Ubuntu Nginx and UFW Baseline

- Installed Nginx on Ubuntu Server
- Created a custom internal SilverLab web page
- Configured UFW with SSH and HTTP allowed
- Validated Nginx service status, web access, and firewall rules

Documentation:

- [Ubuntu Nginx and UFW Baseline](docs/10-ubuntu-nginx-ufw-baseline.md)

### 6. Windows Server VM Baseline

- Created a Windows Server VM in Proxmox
- Corrected the VM guest OS type to Microsoft Windows after identifying the first installation issue
- Loaded the VirtIO SCSI storage driver during Windows Setup so the 60 GiB disk became visible
- Installed Windows Server 2025 Standard Evaluation with Desktop Experience
- Enabled Remote Desktop
- Renamed the server to `SILVER-DC01`
- Validated hostname, IP configuration, gateway, and network connectivity

Documentation:

- [Windows Server VM Baseline](docs/11-windows-server-baseline.md)

## Screenshot Evidence

Curated redacted screenshots are stored in:

```text
assets/screenshots/
```

Screenshot index:

- [Screenshot Evidence README](assets/screenshots/README.md)

## Troubleshooting Tickets

Troubleshooting notes are documented in a ticket-style format to show issue analysis, root cause, resolution, and verification.

| Ticket | Topic |
|---|---|
| [001](docs/tickets/001-laptop2-rj45-fault.md) | Laptop 2 RJ45 / network fault |
| [002](docs/tickets/002-router-replacement.md) | Router replacement |
| [003](docs/tickets/003-proxmox-unreachable-after-subnet-change.md) | Proxmox unreachable after subnet change |
| [004](docs/tickets/004-ubuntu-dhcp-reservation.md) | Ubuntu DHCP reservation |
| [005](docs/tickets/005-windows-server-virtio-driver-disk-detection.md) | Windows Server VirtIO disk driver during installation |

## Command Reference

A project command reference is maintained here:

- [Command Reference](docs/08-command-reference.md)

## Latest Milestone

The latest completed milestone is:

```text
Windows Server VM Baseline
```

This milestone adds a job-relevant Microsoft infrastructure foundation to SilverLab, including Windows Server installation, RDP administration, hostname/network validation, and Proxmox VirtIO driver troubleshooting.

## Next Milestone: Active Directory Domain Services Baseline

The next milestone is to promote the Windows Server VM into the first SilverLab Domain Controller.

Planned implementation:

- Assign a stable IP address or DHCP reservation to `SILVER-DC01`
- Install Active Directory Domain Services
- Promote `SILVER-DC01` to a Domain Controller
- Create the initial lab domain
- Configure DNS as part of the domain controller role
- Create organisational units for users, admins, servers, and workstations
- Create test user and admin accounts
- Validate domain and DNS functionality
- Document screenshots and configuration steps

## Later Roadmap

After Active Directory is stable, the planned direction is:

1. Cross-platform validation between Windows Server and Ubuntu Server
2. Windows client VM and domain join
3. Group Policy basics
4. OPNsense firewall and lab segmentation
5. Backups and restore testing
6. Monitoring/logging with Windows and Linux events
7. Security/SOC-style workflows
8. Automation with PowerShell, Bash, and later Ansible

## Security Principles

SilverLab documentation avoids exposing sensitive information. The repo should not contain:

- Passwords
- Private keys
- API tokens
- Tailscale auth keys
- Public IP addresses
- Email addresses
- Personal addresses
- MAC addresses unless redacted
- Serial numbers
- Router/Wi-Fi passwords
- Browser tabs containing personal information
