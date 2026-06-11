# 04 - TP-Link Archer C6 Router Migration

## Overview

This document records the second major infrastructure milestone for SilverLab: replacing the previous lab router with a TP-Link Archer C6 and migrating the lab network to a new subnet.

The purpose of this phase was to improve lab network stability, restore Proxmox access on the new router, confirm secure remote access through Tailscale, and validate that the Ubuntu Server VM continued working after the subnet change.

## Previous State

The first version of SilverLab used a Technicolor TG582n router for the lab network.

Previous network state:

```text
Lab Wi-Fi: SilverLab
Gateway: 192.168.0.1
Proxmox management IP: 192.168.0.200/24
```

This worked for the initial build, but the router was replaced to improve stability and create a cleaner foundation for future work.

## New Router

The replacement router is:

```text
TP-Link Archer C6
```

The router was configured using stock firmware and the standard setup wizard.

Completed setup choices:

- WAN connection type: Dynamic IP
- Router MAC address: Default MAC address
- Wi-Fi SSID: `SilverHomeLab`
- Automatic updates: Enabled

## Current Network State

| Item | Current Value |
|---|---|
| Router | TP-Link Archer C6 |
| Wi-Fi SSID | `SilverHomeLab` |
| Lab subnet | `192.168.1.x` |
| Router gateway | `192.168.1.1` |
| Proxmox management IP | `192.168.1.200/24` |
| Proxmox local access | Restored |
| Tailscale access | Restored |
| Ubuntu VM | Checked after subnet migration |

## Updated Proxmox Network Configuration

The Proxmox host was updated from the old subnet to the new Archer C6 subnet.

Working configuration:

```text
auto lo
iface lo inet loopback

iface nic1 inet manual

auto vmbr0
iface vmbr0 inet static
        address 192.168.1.200/24
        gateway 192.168.1.1
        bridge-ports nic1
        bridge-stp off
        bridge-fd 0

iface nic0 inet manual

iface nic2 inet manual

source /etc/network/interfaces.d/*
```

## Proxmox Recovery

During the migration, Proxmox temporarily became unreachable because its static management IP and gateway were still configured for the old router subnet.

Cause:

```text
Proxmox still had the old static IP/gateway configuration while the router had moved to the 192.168.1.x network.
```

Resolution:

```text
Updated Proxmox networking to use 192.168.1.200/24 with gateway 192.168.1.1.
```

The change was completed from the physical Proxmox console, then Proxmox was rebooted cleanly to apply the configuration.

## Tailscale Remote Access

After local access was restored, Tailscale was validated again.

Result:

```text
Secure remote access to Proxmox through Tailscale was restored successfully.
```

Security rationale:

```text
Tailscale allows secure remote administration without exposing the Proxmox web interface to the public internet.
```

No public port forwarding was used.

## WAN Link Warning

During router setup, the Archer C6 displayed a warning that the WAN port was communicating with the upstream device at a suboptimal rate.

Likely cause:

```text
Mini switch or older cabling between the Archer C6 WAN side and the upstream home router.
```

Current decision:

```text
Connectivity is stable, so this will be reviewed later as a non-critical optimisation task.
```

## Result

At the end of this phase:

- The TP-Link Archer C6 was installed and configured
- The lab Wi-Fi was changed to `SilverHomeLab`
- The lab network moved to the `192.168.1.x` subnet
- Proxmox local browser access was restored
- Tailscale remote access was confirmed
- The Ubuntu Server VM was checked after the subnet migration

## Skills Practiced

- Router replacement
- Wi-Fi configuration
- WAN/LAN understanding
- Subnet migration
- Static IP and gateway troubleshooting
- Proxmox recovery from physical console
- Secure remote access validation
- Tailscale verification
- Practical network troubleshooting
- Technical documentation
