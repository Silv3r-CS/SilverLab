# Router Replacement and Subnet Migration

This document records the migration from the original router environment to the TP-Link Archer C6 lab router.

## Objective

Replace the original router setup with a more suitable lab router and move the lab network onto a cleaner `192.168.1.0/24` subnet.

## Reason for change

The original router was not a good long-term foundation for the lab. The replacement router provided a cleaner management interface and a more suitable base for DHCP planning, address reservations, and stable lab connectivity.

## New router baseline

| Item | Value |
|---|---|
| Router | TP-Link Archer C6 |
| Lab SSID | `SilverHomeLab` |
| Gateway | `192.168.1.1` |
| DHCP pool | `192.168.1.100-192.168.1.199` |
| Proxmox static IP | `192.168.1.200` |
| Ubuntu reserved IP | `192.168.1.120` |

## Migration issue

After the router migration, the lab subnet changed from the earlier `192.168.0.x` range to the new `192.168.1.x` range. Because Proxmox used a static management IP, it needed to be updated to match the new gateway and subnet.

## Recovery approach

1. Connect locally to the Proxmox host when remote/web access was unavailable.
2. Update the Proxmox management IP and gateway to the new lab subnet.
3. Confirm router gateway connectivity.
4. Confirm Proxmox web access locally from Laptop 1.
5. Confirm secure remote access still worked through Tailscale.
6. Reserve the Ubuntu Server VM IP on the new router.
7. Validate the Ubuntu VM received the expected reserved IP.

## Useful commands

| Command | Purpose | Why it mattered |
|---|---|---|
| `cat /etc/network/interfaces` | View Proxmox network config | Confirmed old/new IP settings |
| `ip route` | Check gateway/default route | Confirmed the host was using the new router gateway |
| `ping -c 4 192.168.1.1` | Test router connectivity | Confirmed Proxmox could reach the router |
| `reboot` | Restart host after network changes | Applied the corrected static network configuration cleanly |
| `ip -br a` | Confirm interface state and addresses | Verified the host/VM network state |

## Outcome

The lab network migration was completed successfully.

Current working access:

```text
Proxmox local access: https://192.168.1.200:8006
Ubuntu Server VM: 192.168.1.120
Router gateway: 192.168.1.1
```

Secure remote access was retained through Tailscale without public port forwarding.

## Skills demonstrated

- Router replacement
- Subnet migration
- Static IP/gateway correction
- DHCP pool planning
- DHCP reservation
- Troubleshooting management access loss
- Validation after infrastructure change
