# 02 - Troubleshooting: Faulty LAN Adapter and USB-to-LAN Fix

## Problem

After installing Proxmox VE on Laptop 2, the built-in LAN adapter appeared to be faulty.

A Proxmox log report showed a network-related `FFFFF` error. The internal adapter was not reliable enough to use as the main Proxmox management interface.

## Investigation

The command below was used to inspect network interfaces:

```bash
ip a
```

The output showed:

```text
nic0: built-in LAN adapter, down
nic1: USB-to-LAN adapter, up and connected to vmbr0
wlo1: built-in Wi-Fi adapter, down
vmbr0: Proxmox bridge, IP 192.168.0.200/24
```

The working path was confirmed by the following:

```text
nic1 ... master vmbr0 state UP
vmbr0 ... inet 192.168.0.200/24
```

## Resolution

A USB-to-LAN adapter was installed and used as the active Proxmox network adapter.

The Proxmox bridge was configured to use `nic1`:

```text
bridge-ports nic1
```

The defective built-in adapter was left unused:

```text
iface nic0 inet manual
```

## Final Working Configuration

```text
auto lo
iface lo inet loopback

iface nic1 inet manual

auto vmbr0
iface vmbr0 inet static
        address 192.168.0.200/24
        gateway 192.168.0.1
        bridge-ports nic1
        bridge-stp off
        bridge-fd 0

iface nic0 inet manual

iface nic2 inet manual

source /etc/network/interfaces.d/*
```

## Result

Proxmox became reachable through the browser again at:

```text
https://192.168.0.200:8006
```

The active network path is now:

```text
Technicolor TG582n / SilverLab
        |
USB-to-LAN adapter: nic1
        |
vmbr0
        |
Proxmox host: 192.168.0.200
```

## Lessons Learned

- A failed physical network adapter can prevent reliable hypervisor access.
- Proxmox management should be bound to a stable physical interface through a bridge.
- USB-to-LAN adapters can be useful as a recovery or replacement interface in a lab.
- `ip a` and `/etc/network/interfaces` are essential tools for Linux network troubleshooting.
- Documenting the fault, investigation, fix, and result makes the project more useful as a portfolio item.

## Skills Demonstrated

- Troubleshooting faulty hardware
- Reading Linux network interface state
- Reconfiguring Proxmox networking
- Understanding Linux bridges
- Validating management access
- Writing professional technical documentation
