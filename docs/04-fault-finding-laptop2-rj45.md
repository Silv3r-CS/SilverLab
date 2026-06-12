# Fault Finding: Laptop 2 RJ45 / Network Adapter Issue

This document records the troubleshooting process around the unreliable built-in RJ45/LAN connection on Laptop 2.

## Problem summary

Laptop 2 is the Proxmox VE host. During the early build, the built-in RJ45/LAN interface did not provide a reliable long-term network path for Proxmox management. This was a critical issue because Proxmox requires stable network access for administration and VM connectivity.

## Impact

- Proxmox web management could become unreachable.
- VM networking would not be reliable.
- Remote administration from Laptop 1 would be disrupted.
- The lab could not progress reliably until host networking was stable.

## Troubleshooting approach

The issue was treated as a practical hardware/network fault rather than only a software configuration problem.

Steps followed:

1. Identify available network interfaces on the Proxmox host.
2. Confirm which interface provides stable physical network connectivity.
3. Move the Proxmox bridge to the working USB-to-LAN adapter.
4. Validate Proxmox management access from Laptop 1.
5. Validate VM network access through `vmbr0`.

## Commands and checks

| Command | Used for | Why it mattered |
|---|---|---|
| `ip -br a` | List interfaces and their state | Identified which interfaces were present and active |
| `ip link` | Show link-level interface status | Helped confirm whether interfaces were up/down |
| `cat /etc/network/interfaces` | Review Proxmox network configuration | Confirmed which physical adapter was attached to `vmbr0` |
| `ping -c 4 192.168.1.1` | Test gateway connectivity | Confirmed the host could reach the router |
| Browser test to Proxmox UI | Validate management access | Confirmed successful outcome from Laptop 1 |

## Resolution

The built-in LAN interface was not used as the active Proxmox bridge port. The working USB-to-LAN adapter was configured as the physical bridge port for `vmbr0`.

## Outcome

- Proxmox management access became stable.
- VMs could use the lab network through the bridge.
- The issue became useful portfolio evidence for hardware fault finding, network troubleshooting, and practical problem solving.

## Skills demonstrated

- Network adapter troubleshooting
- Linux interface validation
- Proxmox bridge configuration
- Hardware workaround planning
- Practical IT support diagnosis
