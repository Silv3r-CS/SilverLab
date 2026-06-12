# Proxmox Installation and Networking

This document records the current Proxmox networking baseline used by SilverLab.

## Objective

Install Proxmox VE on Laptop 2 and provide stable web management access for creating and managing virtual machines.

## Current Proxmox management details

| Item | Value |
|---|---|
| Host role | Virtualization host |
| Node name | `pve` |
| Management URL | `https://192.168.1.200:8006` |
| Bridge | `vmbr0` |
| Active bridge port | USB-to-LAN adapter |
| Gateway | `192.168.1.1` |
| Public exposure | None planned |

## Network interface design

Proxmox uses a Linux bridge called `vmbr0`. The bridge allows virtual machines to behave as if they are connected directly to the lab LAN.

The current design is:

```text
USB-to-LAN adapter -> vmbr0 -> Proxmox host + VMs
```

## Redacted interface configuration

A redacted version of the relevant Proxmox network configuration is stored in:

[`../configs/proxmox-network-interfaces-redacted.txt`](../configs/proxmox-network-interfaces-redacted.txt)

## Commands used during validation

| Command | Purpose | Why it was useful |
|---|---|---|
| `ip -br a` | Show network interfaces and IP addresses in short format | Quickly confirms which interfaces are up and which IP addresses are assigned |
| `ip route` | Show routing table | Confirms the default gateway and network path |
| `cat /etc/network/interfaces` | View Proxmox network configuration | Confirms the bridge, static address, and gateway configuration |
| `ping -c 4 192.168.1.1` | Test router reachability | Validates local LAN connectivity to the gateway |
| `systemctl status pveproxy --no-pager` | Check Proxmox web proxy service | Confirms the Proxmox web UI service is running |
| `ss -lntp \\| grep 8006` | Check if port 8006 is listening | Confirms the Proxmox web interface is accepting local connections |

## Outcome

Proxmox management access was restored and validated on the new lab subnet at:

```text
https://192.168.1.200:8006
```

The Proxmox host now provides the foundation for Ubuntu Server and future Windows Server, Active Directory, monitoring, and firewall lab services.
