# Ticket 001 - Laptop 2 RJ45 Fault / Proxmox Network Instability

| Field | Detail |
|---|---|
| Type | Incident / hardware-network fault |
| Impact | Proxmox management access and VM networking could become unreliable |
| Priority | High, because the Proxmox host is the lab foundation |

## Issue

Laptop 2 was selected as the Proxmox VE host, but the built-in RJ45/LAN interface did not provide a reliable long-term network path.

## Troubleshooting steps

1. Checked available network interfaces.
2. Identified the working USB-to-LAN adapter.
3. Reviewed Proxmox bridge configuration.
4. Moved the active bridge path to the working USB-to-LAN adapter.
5. Validated management access from Laptop 1.

## Commands used

```bash
ip -br a
ip route
cat /etc/network/interfaces
ping -c 4 192.168.1.1
```

## Root cause

The built-in RJ45/LAN interface was not suitable for stable Proxmox networking.

## Resolution

Configured the Proxmox Linux bridge `vmbr0` to use the working USB-to-LAN adapter.

## Verification

Proxmox became reachable again from Laptop 1 and the host could communicate with the lab router.

## Skills demonstrated

- Hardware fault finding
- Network interface validation
- Proxmox bridge troubleshooting
- Practical support-style diagnosis
