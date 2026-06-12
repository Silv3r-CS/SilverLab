# Screenshots

This folder contains selected redacted screenshots used as visual evidence for the SilverLab documentation baseline.

## Current selected screenshots

| File | Purpose |
|---|---|
| `01-archer-c6-dhcp-pool-ubuntu-reservation-redacted.png` | Shows DHCP pool planning and Ubuntu reservation evidence |
| `02-ubuntu-reserved-ip-validation.png` | Shows Ubuntu receiving the reserved IP address |
| `05-ubuntu-qemu-guest-agent-active.png` | Shows QEMU Guest Agent running in Ubuntu |
| `06-ubuntu-server-baseline-checks.png` | Shows baseline Linux checks such as hostname, disk, memory, and uptime |
| `07-ubuntu-ssh-access-from-laptop1-redacted.png` | Shows SSH administration from Laptop 1 to Ubuntu Server |
| `12-proxmox-service-connectivity-checks-redacted.png` | Shows Proxmox service/connectivity validation |

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

Private lab IP addresses such as `192.168.1.120` and `192.168.1.200` are acceptable because they are part of the documented internal lab design.
