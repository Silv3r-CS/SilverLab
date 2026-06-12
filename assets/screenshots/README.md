# SilverLab Screenshot Evidence

This folder contains selected, redacted screenshots used as visual evidence for the SilverLab documentation baseline. The screenshots are ordered to tell the story of the current foundation build: router migration, Proxmox networking, Ubuntu Server baseline, remote access, and VM management.

## Screenshot index

| # | File | Purpose | Skill demonstrated |
|---:|---|---|---|
| 01 | `01-router-dhcp-pool-and-ubuntu-reservation-redacted.png` | Shows TP-Link Archer C6 DHCP scope and Ubuntu Server reservation. | DHCP planning, IP address management, router administration |
| 02 | `02-ubuntu-reserved-ip-validation.png` | Shows Ubuntu receiving the reserved `192.168.1.120/24` address. | Linux network validation |
| 03 | `03-ubuntu-migration-validation-current-network.png` | Shows Ubuntu on the new `192.168.1.x` network, default route via `192.168.1.1`, and successful router ping. | Migration validation, Linux routing checks |
| 04 | `04-proxmox-migration-validation-shell.png` | Shows Proxmox on `192.168.1.200/24`, gateway `192.168.1.1`, persistent `vmbr0` config, and router reachability. | Proxmox CLI validation, persistent network configuration |
| 05 | `05-proxmox-linux-bridge-vmbr0-gui.png` | Shows the Proxmox `vmbr0` Linux bridge configuration in the GUI. | Proxmox networking, bridge configuration |
| 06 | `06-proxmox-network-interfaces-redacted.png` | Shows the Proxmox network interface list and `vmbr0` using `nic1`; adapter identifiers are redacted. | Hardware fault workaround, bridge-to-adapter mapping |
| 07 | `07-proxmox-node-summary-redacted.png` | Shows the Proxmox host/node summary and resource status. | Hypervisor monitoring, resource awareness |
| 08 | `08-proxmox-storage-summary-redacted.png` | Shows `local` and `local-lvm` storage definitions. | Storage layout awareness, VM disk planning |
| 09 | `09-ubuntu-vm-hardware-options-redacted.png` | Shows the Ubuntu VM hardware configuration, including CPU, RAM, disk, and bridge networking; VM MAC is redacted. | VM sizing, virtual hardware, network bridge assignment |
| 10 | `10-ubuntu-qemu-guest-agent-active.png` | Shows QEMU Guest Agent running inside Ubuntu. | Guest integration, service validation |
| 11 | `11-ubuntu-server-initial-baseline-checks.png` | Shows initial Ubuntu baseline checks such as hostname, disk, memory, and uptime. | Linux administration, baseline verification |
| 12 | `12-ubuntu-ssh-access-from-laptop1-redacted.png` | Shows SSH administration from Laptop 1 to Ubuntu Server; fingerprint details are redacted. | Remote administration, SSH access validation |
| 13 | `13-tailscale-access-controls-redacted.png` | Shows redacted Tailscale access-control evidence for secure remote-access planning. | VPN/remote-access awareness, security documentation |

## Redaction policy

Screenshots must not include:

- Passwords
- Private keys
- API tokens
- Tailscale auth keys
- Public IP addresses
- Email addresses
- Personal addresses
- MAC addresses unless intentionally redacted
- Browser tabs with personal/private information
- Serial numbers
- Wi-Fi/router passwords

Private lab IP addresses such as `192.168.1.120` and `192.168.1.200` are acceptable because they are part of the documented internal lab design.

## Notes

Some early Ubuntu screenshots show the older `192.168.0.x` network. These are retained as initial baseline evidence and are supplemented by current `192.168.1.x` migration validation screenshots.
