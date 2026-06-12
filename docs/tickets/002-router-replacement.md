# Ticket 002 - Router Replacement and Lab Network Migration

| Field | Detail |
|---|---|
| Type | Infrastructure change |
| Impact | Lab subnet, gateway, DHCP, Proxmox static IP, VM addressing |
| Priority | High |

## Issue

The original router was not a suitable long-term base for the lab. The network was migrated to a TP-Link Archer C6 router.

## Change summary

- New lab router installed.
- Lab SSID configured.
- Gateway moved to `192.168.1.1`.
- DHCP pool set to `192.168.1.100-192.168.1.199`.
- Proxmox management IP updated to `192.168.1.200`.
- Ubuntu VM reserved at `192.168.1.120`.

## Commands/checks used

```bash
cat /etc/network/interfaces
ip route
ping -c 4 192.168.1.1
ip -br a
```

## Outcome

The lab network became stable on the new subnet and Proxmox management access was restored.

## Skills demonstrated

- Network migration
- DHCP planning
- Static IP planning
- Router configuration
- Change validation
