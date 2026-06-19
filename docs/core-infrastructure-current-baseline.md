# Core Infrastructure Current Baseline

This document records the current SilverLab infrastructure baseline after the hardware upgrade and core network redesign.

## Purpose

The purpose of this milestone is to show a stable, documented infrastructure foundation before adding more advanced services such as monitoring, IDS, ticketing, MDM, backups, or security tooling.

## Hardware Roles

| Device | Name | Role |
|---|---|---|
| Laptop 1 | **SILVER-KALI-CLIENT** | Endpoint/client VM host and Kali admin/security workstation. |
| Laptop 2 | **SILVER-PVE01** | Proxmox VE infrastructure host. |

## Proxmox Baseline

**SILVER-PVE01** now has approximately 16 GiB RAM available to Proxmox. This makes the core infrastructure more practical because pfSense, Windows Server, and Ubuntu services can run together with more headroom than the original 8 GiB baseline.

Current core VM roles:

| VM | Role | Notes |
|---|---|---|
| **SILVER-FW01** | pfSense firewall/router/VPN | Provides LAN gateway, DHCP, DNS forwarding, and OpenVPN. |
| **SILVER-DC01** | Windows Server domain controller | Provides AD DS, DNS for `silverlab.local`, and GPO. |
| **SILVER-WEB01** | Ubuntu/Nginx internal web server | Provides internal Linux/web evidence. |

## Network Design

| Network | Purpose |
|---|---|
| Home / management side | Proxmox management and pfSense WAN uplink. |
| Protected SilverLab LAN | Internal lab network behind pfSense. |

Key addresses:

| Component | Address / role |
|---|---|
| Home edge router | `192.168.0.1` |
| pfSense WAN | `192.168.0.2` |
| pfSense LAN | `192.168.1.1` |
| SilverLab access point | `192.168.1.2` |
| SILVER-DC01 | `192.168.1.10` |
| SILVER-WEB01 | Around `192.168.1.120` |
| DHCP scope | `192.168.1.160 - 192.168.1.199` |

## DNS Design

Normal clients use pfSense DNS at `192.168.1.1`. pfSense forwards the `silverlab.local` domain to SILVER-DC01 at `192.168.1.10`.

This design keeps normal internet DNS working even when clients are not directly configured to use the domain controller as their primary DNS server.

## Evidence Captured

- Proxmox showing approx. 16 GiB RAM available.
- Core VM list including Ubuntu, Windows Server, and pfSense.
- Windows Server network validation.
- AD/GPO validation evidence.
- OpenVPN external-client validation evidence.

## Portfolio Skills Demonstrated

- Hypervisor management
- VM resource planning
- Routed/firewalled lab design
- DHCP and DNS design
- Windows Server administration
- Linux service hosting
- Remote access planning
- Evidence-based documentation
