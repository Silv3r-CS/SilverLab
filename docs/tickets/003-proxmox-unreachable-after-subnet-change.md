# Ticket 003 - Proxmox Unreachable After Subnet Change

| Field | Detail |
|---|---|
| Type | Incident after infrastructure change |
| Impact | Proxmox web UI unreachable until static network config was corrected |
| Priority | High |

## Issue

After moving to the new router/subnet, Proxmox still required network settings compatible with the old subnet. Because Proxmox used a static management address, it had to be manually aligned with the new `192.168.1.0/24` network.

## Troubleshooting steps

1. Recognised the subnet mismatch after router replacement.
2. Accessed Proxmox locally.
3. Reviewed network configuration.
4. Updated Proxmox static IP/gateway to the new lab network.
5. Rebooted/applied network changes.
6. Tested browser access from Laptop 1.

## Commands/checks used

```bash
cat /etc/network/interfaces
ip route
ping -c 4 192.168.1.1
reboot
```

## Resolution

Proxmox was placed on the correct subnet with management access at:

```text
https://192.168.1.200:8006
```

## Skills demonstrated

- Static IP troubleshooting
- Gateway validation
- Recovery after network change
- Management-plane access restoration
