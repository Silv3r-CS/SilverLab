# 01 - Initial Lab Build

## Overview

This document records the first working stage of the SilverLab homelab.

The objective of this phase was to install Proxmox VE on a repurposed laptop, establish browser-based management access from another laptop, and create a dedicated lab network that can later host virtual machines and services.

## Hardware Used

| Device | Role |
|---|---|
| Laptop 1 | Admin workstation |
| Laptop 2 | Proxmox VE host |
| USB-to-LAN adapter | Replacement network adapter for Proxmox host |
| Technicolor TG582n | Lab router / access point |
| Home router | Upstream internet connection |

## Current Design

```text
Home Router / Main Internet
        |
Technicolor TG582n
SilverLab Wi-Fi / Lab Network
        |
USB-to-LAN Adapter
        |
Laptop 2 - Proxmox VE Host
IP: 192.168.0.200/24
```

## Proxmox Host

Laptop 2 is running Proxmox VE and is reachable from Laptop 1 using:

```text
https://192.168.0.200:8006
```

The host is configured with a static IP address:

```text
192.168.0.200/24
```

The default gateway is:

```text
192.168.0.1
```

## Network Bridge

Proxmox uses a Linux bridge named:

```text
vmbr0
```

The bridge is attached to the working USB-to-LAN adapter:

```text
nic1
```

This allows both Proxmox management traffic and future VM traffic to use the same working physical network adapter.

## Confirmed Network Configuration

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

## Storage

The Proxmox host uses a 256 GB SSD. The usable Linux-reported size is approximately 238.5 GiB.

The storage is split between Proxmox system storage and VM disk storage.

```text
Proxmox root:  ~69.5 GiB
VM disk pool: ~141.5 GiB
Swap:           ~7.6 GiB
```

The VM disk pool is available through:

```text
local-lvm
```

## Result

At the end of this phase:

- Proxmox was installed successfully
- Laptop 1 could access the Proxmox web interface
- The defective internal LAN adapter was bypassed
- The USB-to-LAN adapter became the active Proxmox network path
- The SilverLab Wi-Fi network was created for lab access
- The Proxmox host was ready for its first VM

## Skills Practiced

- Hypervisor installation
- Network adapter troubleshooting
- Linux interface inspection
- Proxmox bridge configuration
- Static IP addressing
- Router repurposing
- Infrastructure documentation
