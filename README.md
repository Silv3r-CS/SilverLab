# SilverLab Homelab

SilverLab is a practical IT infrastructure and cyber-security learning lab built on repurposed laptop hardware. The project is designed to demonstrate entry-level IT support, junior infrastructure, networking, Linux administration, documentation, troubleshooting, secure remote access, and future cyber/SOC skills.

The lab is intentionally documented like a small professional IT environment: hardware inventory, network topology, change notes, incident-style troubleshooting, command references, configuration evidence, and implementation roadmap.

## Current lab status

| Area | Status |
|---|---|
| Proxmox VE host | Installed on Laptop 2 and reachable on the lab network |
| Lab router | Migrated to TP-Link Archer C6 on the `192.168.1.0/24` lab subnet |
| Proxmox management IP | `192.168.1.200` |
| Ubuntu Server VM | Built, baselined, reachable over SSH |
| Ubuntu VM reserved IP | `192.168.1.120` |
| Secure remote access | Tailscale used for private remote access; no public port forwarding |
| Documentation state | Rebuilt into a clean baseline structure |
| Next technical build | Ubuntu Nginx internal web service + UFW firewall baseline |

## High-level architecture

```text
Internet / Upstream home network
        |
        | WAN uplink
        v
TP-Link Archer C6 lab router
Gateway: 192.168.1.1
DHCP pool: 192.168.1.100-192.168.1.199
        |
        | LAN
        v
Laptop 2 - Proxmox VE host
Management: 192.168.1.200
Bridge: vmbr0 through working USB-to-LAN adapter
        |
        +-- Ubuntu Server VM: 192.168.1.120
        +-- Future Windows Server VM
        +-- Future monitoring/SIEM services

Laptop 1 - Admin workstation
Used for browser access, SSH, GitHub documentation, screenshots, and lab administration.
```

See the full topology document in [`docs/02-network-topology.md`](docs/02-network-topology.md).

## Skills demonstrated so far

- Proxmox VE installation and basic host administration
- Network adapter fault finding and workaround using USB-to-LAN
- Linux network validation using command-line tools
- Static management IP planning for Proxmox
- DHCP pool planning and DHCP reservation for the Ubuntu VM
- Router replacement and subnet migration
- Ubuntu Server VM deployment and baseline checks
- SSH validation from an admin workstation
- QEMU Guest Agent installation and validation
- Tailscale secure remote access model without public port forwarding
- Markdown documentation, GitHub project structure, visual evidence handling, and privacy-aware redaction

## Documentation index

| Document | Purpose |
|---|---|
| [`docs/00-project-roadmap.md`](docs/00-project-roadmap.md) | Current and planned implementation roadmap |
| [`docs/01-hardware-inventory.md`](docs/01-hardware-inventory.md) | Devices, roles, and hardware details used in the lab |
| [`docs/02-network-topology.md`](docs/02-network-topology.md) | Current physical and logical network design |
| [`docs/03-proxmox-installation-and-networking.md`](docs/03-proxmox-installation-and-networking.md) | Proxmox deployment and management networking |
| [`docs/04-fault-finding-laptop2-rj45.md`](docs/04-fault-finding-laptop2-rj45.md) | Defective RJ45 fault finding and workaround |
| [`docs/05-router-replacement-and-subnet-migration.md`](docs/05-router-replacement-and-subnet-migration.md) | Router replacement and migration from old subnet to new subnet |
| [`docs/06-ubuntu-server-baseline.md`](docs/06-ubuntu-server-baseline.md) | Ubuntu VM deployment, SSH validation, guest agent, baseline tools |
| [`docs/07-secure-remote-access-tailscale.md`](docs/07-secure-remote-access-tailscale.md) | Secure remote access design using Tailscale |
| [`docs/08-command-reference.md`](docs/08-command-reference.md) | Bash/Linux/Proxmox command reference with explanations |
| [`docs/09-next-implementation-plan.md`](docs/09-next-implementation-plan.md) | Updated plan focused on job-market skill gaps |
| [`docs/tickets/`](docs/tickets) | Incident-style troubleshooting notes |

## Evidence approach

Screenshots are used only where they prove functionality. Historical screenshots are not recreated if they were missed. Instead, current-state screenshots are used to demonstrate that the lab is working.

Current selected visual evidence is stored in [`assets/screenshots/`](assets/screenshots/). Sensitive information such as passwords, keys, tokens, public IPs, personal details, MAC addresses where appropriate, and Tailscale user/tailnet details has been excluded or redacted.

## Security approach

- Proxmox is not exposed directly to the public internet.
- Remote access is handled through Tailscale.
- Public domain usage is planned only for safe portfolio/demo purposes later.
- No passwords, private keys, secrets, tokens, or personal identifiers are intentionally documented.

## Next milestone

The next planned technical contribution is:

```text
Ubuntu Nginx internal web service + UFW firewall baseline
```

This will add a simple internal service to the Ubuntu VM, demonstrate Linux service deployment, firewall configuration, and web access validation from Laptop 1.
