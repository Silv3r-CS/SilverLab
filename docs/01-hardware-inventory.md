# Hardware Inventory

This document records the physical devices used in the SilverLab environment. The format is similar to a lightweight asset inventory.

## Laptop 1 - Admin workstation

| Item | Detail |
|---|---|
| Role | Admin workstation |
| RAM | 16 GB |
| Use | Browser access to Proxmox, SSH into VMs, GitHub documentation, screenshots, downloads/uploads, and general administration |
| Operating systems | Windows used as the main comfort/admin environment; Kali/Linux partition available for lab/security tasks |
| Lab role | Not currently treated as a monitored production endpoint/log source unless explicitly added later |

## Laptop 2 - Proxmox host

| Item | Detail |
|---|---|
| Role | Proxmox VE virtualization host |
| RAM | 8 GB |
| Storage | Internal SSD, approximately 238 GB physical capacity |
| Proxmox management IP | `192.168.1.200` |
| Network bridge | `vmbr0` |
| Active physical network path | USB-to-LAN adapter bridged to `vmbr0` |
| Known issue | Built-in RJ45/LAN port was unreliable or unsuitable for stable Proxmox networking |
| Resolution | Use working USB-to-LAN adapter as the active bridge port |

## TP-Link Archer C6 router

| Item | Detail |
|---|---|
| Role | Lab router |
| Lab SSID | `SilverHomeLab` |
| Gateway | `192.168.1.1` |
| DHCP pool | `192.168.1.100` to `192.168.1.199` |
| Proxmox address approach | Static management IP outside the DHCP pool: `192.168.1.200` |
| Ubuntu address approach | DHCP reservation at `192.168.1.120` |

## Ubuntu Server VM

| Item | Detail |
|---|---|
| VM name | `SilverServer-Ubuntu` |
| Hostname | `homelab-silver` |
| Role | First Linux server VM |
| vCPU | 2 cores |
| RAM | 2 GB allocated |
| Disk | 32 GB virtual disk on Proxmox `local-lvm` |
| Network | VirtIO NIC connected to `vmbr0` |
| IP address | `192.168.1.120` |
| Services | SSH, QEMU Guest Agent, baseline admin tools |

## SilverStore external drive

| Item | Detail |
|---|---|
| Role | Future backup/storage milestone |
| Capacity | Approximately 931 GB available as external storage |
| Planned use | Proxmox VM backups, ISO/archive storage, restore testing, and possibly a lightweight file-server VM/LXC |
| Not planned | Active VM disks unless the drive is confirmed suitable for that workload |

## Hardware lessons learned

- Laptop-based homelabs are useful, but network adapter reliability matters.
- A small RAM host requires staged deployment: one or two VMs running at a time, with powered-off VMs used as available scenarios.
- External storage is best introduced as a backup/restore milestone rather than immediately used for active VM disks.
