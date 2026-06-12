# Next Implementation Plan

This plan is focused on closing practical skill gaps for entry-level IT support, service desk, junior infrastructure, and future cyber/SOC roles.

## Priority 1 - Ubuntu Nginx internal web service

Build a simple internal web page on the Ubuntu Server VM.

Planned result:

```text
http://192.168.1.120
```

The page should show:

- Server role
- Hostname
- Services running
- Lab purpose
- Date/version of the milestone

Skills demonstrated:

- Linux service installation
- Web service basics
- Browser-based validation
- Service troubleshooting
- Documentation

## Priority 2 - UFW firewall baseline

Enable and configure UFW on Ubuntu.

Planned rules:

- Allow SSH
- Allow HTTP
- Deny unnecessary inbound traffic

Skills demonstrated:

- Host firewalling
- Least privilege
- Security basics
- Service access validation

## Priority 3 - Ticket-style troubleshooting notes

Create incident-style documentation for real lab issues.

Topics:

- RJ45/network adapter fault
- Router replacement
- Subnet migration
- DHCP reservation
- QEMU Guest Agent validation

Skills demonstrated:

- Service desk process
- Incident documentation
- Root-cause analysis
- Clear communication

## Priority 4 - Windows Server VM baseline

Create a Windows Server VM carefully due to the 8 GB RAM limit on Laptop 2.

Initial target:

- Install Windows Server
- Rename server
- Configure network address/reservation
- Take Proxmox snapshot
- Document baseline

Skills demonstrated:

- Windows Server installation
- Virtualization resource planning
- Server baseline documentation

## Priority 5 - Active Directory basics

After Windows Server is stable, create a simple AD lab.

Initial target:

- Domain Controller
- Lab domain
- Users
- Groups
- Organisational Units
- Basic Group Policy concepts

Skills demonstrated:

- Identity administration
- Windows infrastructure basics
- Helpdesk-relevant account management

## Priority 6 - Backup and restore

Use SilverStore for a backup milestone.

Initial target:

- Proxmox VM backup
- Basic retention approach
- Restore test
- Document recovery result

Skills demonstrated:

- Backup operations
- Disaster recovery
- Infrastructure reliability

## Priority 7 - Monitoring/SIEM

Add monitoring after core services are stable.

Possible tools:

- Splunk
- Wazuh
- Lightweight log forwarding first

Skills demonstrated:

- Log analysis
- Security monitoring
- Incident triage
- SOC pathway

## Priority 8 - Domain and portfolio integration

Use `createsomethingnice.com` later for public portfolio value.

Recommended safe use:

- GitHub Pages portfolio
- Project landing page
- DNS practice
- HTTPS/TLS

Do not expose Proxmox publicly.

## Priority 9 - OPNsense and segmentation

Wait until a second USB-to-LAN adapter is available.

Skills demonstrated later:

- Firewalling
- Routing
- Segmentation
- Lab zones
- Network security
