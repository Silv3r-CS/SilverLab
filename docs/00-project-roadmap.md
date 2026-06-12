# SilverLab Project Roadmap

This roadmap reflects the current direction of the SilverLab homelab after the documentation baseline rebuild.

## Aim

Build a realistic, well-documented home IT lab that supports applications for entry-level IT support, service desk, desktop support, junior infrastructure, technical support, and future junior cyber/SOC roles.

## Current implementation phase

| Priority | Element | Purpose | Status |
|---:|---|---|---|
| 1 | Clean GitHub documentation baseline | Make the repo employer-readable and security-aware | In progress |
| 2 | Current topology and hardware inventory | Explain what is being used and why | In progress |
| 3 | Router migration documentation | Show network change and recovery process | Complete/documenting |
| 4 | Ubuntu Server baseline | Linux server administration foundation | Complete/documenting |
| 5 | Command reference | Show command understanding, not just copy/paste use | In progress |
| 6 | Nginx internal web service | Demonstrate Linux service deployment | Next |
| 7 | UFW firewall | Demonstrate host firewall rules and least privilege | Next |
| 8 | Ticket-style troubleshooting notes | Show service-desk process and incident documentation | In progress |

## Near-term job-focused milestones

These are the most valuable next steps before applying for entry-level IT roles.

| Priority | Milestone | Skills demonstrated |
|---:|---|---|
| 1 | Ubuntu Nginx + UFW | Linux services, firewalling, service testing, logs |
| 2 | Structured troubleshooting tickets | Incident handling, root-cause analysis, documentation |
| 3 | Windows Server VM baseline | Windows Server installation, VM resource planning |
| 4 | Active Directory basics | Users, groups, OUs, identity administration |
| 5 | Backup and restore test | Reliability, recovery, infrastructure operations |
| 6 | Monitoring/log collection | SOC pathway, logs, visibility, alert investigation |
| 7 | Microsoft 365 / Entra ID learning plan | Modern cloud identity awareness |
| 8 | Domain/portfolio integration | DNS, HTTPS, GitHub Pages, public portfolio presentation |

## Later milestones

| Milestone | Notes |
|---|---|
| OPNsense firewall VM | Wait until a second USB-to-LAN adapter is available for proper WAN/LAN separation |
| Network segmentation | Build after OPNsense or once VLAN-style segmentation is practical |
| Splunk or Wazuh | Add once core infrastructure is stable |
| Docker services | Add after Linux service and firewall basics are documented |
| `createsomethingnice.com` integration | Use for a safe public portfolio or demo page, not direct Proxmox exposure |

## Guiding rule

Each milestone should produce:

1. A short technical write-up
2. Commands used and why they were used
3. A small number of redacted screenshots showing functionality
4. A brief skills-demonstrated section
5. A clean Git commit
