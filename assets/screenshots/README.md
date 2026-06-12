# Screenshots

This folder contains selected redacted screenshots used as visual evidence for the SilverLab documentation.

## Screenshot index

| File | Purpose |
|---|---|
| `01-router-dhcp-pool-and-ubuntu-reservation-redacted.png` | Archer C6 DHCP pool planning and Ubuntu Server IP reservation. |
| `02-ubuntu-reserved-ip-validation.png` | Ubuntu Server receiving the reserved IP address. |
| `03-ubuntu-migration-validation-current-network.png` | Ubuntu Server migrated successfully to the `192.168.1.x` lab network. |
| `04-proxmox-migration-validation-shell.png` | Proxmox host migrated to `192.168.1.x` with shell validation and gateway ping. |
| `05-proxmox-linux-bridge-vmbr0-gui.png` | Proxmox `vmbr0` Linux bridge configuration in the GUI. |
| `06-proxmox-network-interfaces-redacted.png` | Redacted Proxmox network interface list showing active bridge path. |
| `07-proxmox-node-summary-redacted.png` | Proxmox node summary and host resource health. |
| `08-proxmox-storage-summary-redacted.png` | Proxmox storage layout with `local` and `local-lvm`. |
| `09-ubuntu-vm-hardware-options-redacted.png` | Ubuntu VM hardware/options configuration in Proxmox. |
| `10-ubuntu-qemu-guest-agent-active.png` | QEMU Guest Agent active inside Ubuntu Server. |
| `11-ubuntu-server-initial-baseline-checks.png` | Ubuntu baseline checks: hostname, disk, memory, and uptime. |
| `12-ubuntu-ssh-access-from-laptop1-redacted.png` | SSH administration from Laptop 1 to Ubuntu Server. |
| `13-tailscale-access-controls-redacted.png` | Redacted Tailscale secure remote-access evidence. |
| `15-nginx-installed-service-active.png` | Nginx service active and running on Ubuntu Server. |
| `16-silverlab-nginx-webpage-working.png` | Custom SilverLab internal web page reachable from Laptop 1. |
| `17-nginx-custom-page-validation.png` | Nginx custom index page validation/update evidence. |
| `18-ufw-firewall-rules-ssh-http.png` | UFW active with SSH/OpenSSH and HTTP/Nginx HTTP allowed. |
| `19-windows-server-vm-creation-summary-redacted.png` | Windows Server VM hardware summary: 4 GB RAM, 2 cores, 60 GB disk, OVMF/q35, VirtIO SCSI, and `vmbr0`. |
| `20-windows-server-rdp-access-from-laptop1.png` | Remote Desktop access from Laptop 1 to the Windows Server VM. |
| `21-windows-server-hostname-network-baseline.png` | Windows Server hostname, IP configuration, gateway, and router connectivity validation. |


## Redaction policy

Screenshots should not include:

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

Private lab IP addresses such as `192.168.1.120`, `192.168.1.154`, and `192.168.1.200` are acceptable because they are part of the documented internal lab design.

## Notes

- Screenshot numbering follows the project evidence timeline. Number `14` is intentionally unused because the pre-Nginx snapshot screenshot was not required for the final evidence set.
- The Windows Server baseline evidence focuses on successful installation, RDP administration, hostname configuration, and network validation.
