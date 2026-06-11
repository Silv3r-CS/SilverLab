# SilverLab Screenshots

This folder contains portfolio-safe screenshots for SilverLab Contribution 02.

These images are intended to support the documented milestone covering:

- TP-Link Archer C6 router migration
- `SilverHomeLab` Wi-Fi validation
- Proxmox access restoration
- Tailscale secure remote access validation
- Ubuntu Server VM baseline
- QEMU Guest Agent validation
- Ubuntu DHCP/address reservation

## Screenshot Index

| File | Caption | Use |
|---|---|---|
| `archer-c6-setup-success-wan-warning.png` | TP-Link Archer C6 setup completed successfully, with WAN-side link-rate warning noted for later cabling/switch optimisation. | Router migration evidence |
| `archer-c6-dynamic-ip-default-mac-redacted.png` | Archer C6 WAN setup using Dynamic IP and default MAC address. MAC details have been redacted. | Router setup evidence |
| `laptop1-wifi-link-speed-866mbps.png` | Laptop 1 Wi-Fi link speed showing strong connection to the new router. | Wi-Fi validation evidence |
| `proxmox-login-over-tailscale-redacted.png` | Proxmox web interface accessed through the secure remote-access path. Browser/IP details are redacted/cropped. | Secure access evidence |
| `tailscale-status-proxmox-active-redacted.png` | Proxmox host active in Tailscale after the router/subnet migration. Tailscale IPs and user/tailnet details are redacted. | Tailscale validation evidence |
| `ubuntu-server-ssh-access-from-laptop1.png` | SSH access from Laptop 1 to the Ubuntu Server VM. | Linux remote administration evidence |
| `ubuntu-server-baseline-checks.png` | Ubuntu Server baseline checks showing hostname, IP, disk, memory, swap, and uptime. | Server baseline evidence |
| `ubuntu-qemu-guest-agent-active.png` | QEMU Guest Agent active and running inside the Ubuntu Server VM. | Proxmox guest integration evidence |
| `ubuntu-reserved-ip-192-168-1-120.png` | Ubuntu Server VM showing reserved DHCP address `192.168.1.120/24` on interface `ens18`. | DHCP reservation evidence |
| `kali-proxmox-tailscale-troubleshooting-redacted.png` | Kali-to-Proxmox Tailscale troubleshooting output with sensitive IPs/device details redacted. | Troubleshooting evidence |
| `tcpdump-tailscale-traffic-redacted.png` | `tcpdump` packet capture used during Tailscale troubleshooting, with sensitive IPs redacted. | Network troubleshooting evidence |

## Privacy Notes

Screenshots have been selected and/or redacted to avoid publishing sensitive details such as:

- Passwords
- Public IP addresses
- Tailscale IPs
- Tailscale tailnet/user details
- Router MAC address
- Browser URL details
- Private browser tabs/bookmarks
- Wi-Fi passwords
- Router admin passwords
- Serial numbers

Before committing future screenshots, review them carefully and crop or blur anything private.
