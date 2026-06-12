# Network Topology

SilverLab currently uses a simple flat lab network that is stable enough for core IT support and infrastructure learning. Segmentation will be introduced later when the required hardware is available.

## Current logical network

```text
Internet / upstream home network
        |
        | WAN uplink
        v
TP-Link Archer C6 lab router
Gateway: 192.168.1.1
DHCP pool: 192.168.1.100-192.168.1.199
        |
        | Lab LAN
        v
Laptop 2 - Proxmox VE host
Management IP: 192.168.1.200
Bridge: vmbr0
Physical bridge port: working USB-to-LAN adapter
        |
        +-- Ubuntu Server VM: 192.168.1.120
        +-- Future Windows Server VM
        +-- Future monitoring/SIEM VM or container services

Laptop 1 - Admin workstation
Used for web management, SSH, documentation, screenshots, and validation.
```

## Addressing plan

| Device/service | Addressing method | Current address |
|---|---|---|
| Router gateway | Static router LAN address | `192.168.1.1` |
| DHCP pool | Router-managed DHCP range | `192.168.1.100-192.168.1.199` |
| Proxmox VE | Static IP outside DHCP pool | `192.168.1.200` |
| Ubuntu Server VM | DHCP reservation | `192.168.1.120` |
| Future Windows Server VM | Planned static or reservation | To be assigned |

## Why Proxmox is outside the DHCP pool

Proxmox is the management layer for the lab. It needs a stable address so it can always be reached for administration. Placing it at `192.168.1.200` while the DHCP pool ends at `192.168.1.199` reduces the chance of address conflict.

## Current limitations

- The lab currently uses a flat network without VLANs or separate firewall zones.
- OPNsense and segmentation are planned later, after a second USB-to-LAN adapter is available.
- Proxmox is not exposed through public port forwarding.

## Diagram files

- Mermaid source: [`../assets/diagrams/current-topology.mmd`](../assets/diagrams/current-topology.mmd)
- PNG version: [`../assets/diagrams/current-topology.png`](../assets/diagrams/current-topology.png)
