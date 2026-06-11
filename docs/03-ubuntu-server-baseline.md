# 03 - Ubuntu Server VM Baseline

## Overview

This document records the first Ubuntu Server VM baseline for SilverLab.

The purpose of this phase was to create a lightweight Linux server VM in Proxmox, confirm network access, enable SSH administration, install useful troubleshooting tools, validate QEMU Guest Agent communication, and create a clean baseline snapshot.

## VM Role

The Ubuntu Server VM is the first general-purpose Linux server in SilverLab.

It will be used for:

- Linux administration practice
- SSH administration
- Network testing
- Future service deployment
- Future monitoring/logging practice
- A clean baseline for rollback and recovery testing

## VM Configuration

| Setting | Value |
|---|---|
| VM name | `SilverServer-Ubuntu` |
| Hostname | `homelab-silver` |
| CPU | 2 cores |
| RAM | 2 GiB |
| Disk | 32 GiB |
| Storage | `local-lvm` |
| Network | VirtIO adapter on `vmbr0` |
| QEMU Agent option | Enabled in Proxmox |
| SSH | Enabled during installation |

The VM was kept lightweight because the Proxmox host has 8 GB RAM and needs to support multiple future lab services carefully.

## Software Installed

Core administration and troubleshooting tools were installed:

```text
curl
wget
git
net-tools
dnsutils
traceroute
nmap
htop
qemu-guest-agent
```

## SSH Validation

SSH access from Laptop 1 to the Ubuntu Server VM was confirmed.

This proves that the VM can be administered remotely from the admin workstation, rather than only through the Proxmox console.

Validated outcome:

```text
Laptop 1 can open an SSH session to the Ubuntu Server VM.
```

## QEMU Guest Agent Validation

QEMU Guest Agent was installed and started inside the Ubuntu Server VM.

The service was validated as active, and Proxmox communication with the guest was confirmed.

Why this matters:

- Proxmox can communicate more cleanly with the VM.
- Proxmox can report guest information more accurately.
- Clean shutdowns and management actions are improved.
- Snapshots and backups are better coordinated.

## Baseline Snapshot

After SSH access and QEMU Guest Agent were confirmed, a baseline snapshot was created.

Snapshot name:

```text
ubuntu-baseline-ssh-qemu-agent-working
```

Snapshot purpose:

```text
Clean Ubuntu Server baseline after package updates, successful SSH access, and validated QEMU Guest Agent communication.
```

This provides a safe rollback point before additional services are installed.

## Result

At the end of this phase:

- Ubuntu Server was installed successfully
- The VM was reachable on the lab network
- SSH access from Laptop 1 was confirmed
- Core troubleshooting tools were installed
- QEMU Guest Agent was installed and validated
- A clean baseline snapshot was created

## Skills Practiced

- Creating a Proxmox VM
- Installing Ubuntu Server
- Allocating VM resources for limited hardware
- Configuring SSH access
- Installing Linux administration tools
- Validating services with `systemctl`
- Understanding QEMU Guest Agent
- Creating a safe baseline snapshot
- Documenting a server build for portfolio evidence
