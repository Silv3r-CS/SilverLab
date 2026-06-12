# Next Implementation Plan

## Immediate Priority: Active Directory Domain Services Baseline

The next SilverLab milestone is to configure `SILVER-DC01` as the first Windows Domain Controller.

## Why this is next

Active Directory, DNS, users, groups, permissions, and Windows Server administration appear frequently in entry-level IT Support, Service Desk, Desktop Support, and Junior Infrastructure job adverts. Completing this milestone will make SilverLab more directly relevant for job applications.

## Planned Steps

1. Give `SILVER-DC01` a stable IP address or DHCP reservation.
2. Install the Active Directory Domain Services role.
3. Promote the server to a Domain Controller.
4. Create the initial lab domain.
5. Configure and validate DNS.
6. Create OUs for users, admins, servers, and workstations.
7. Create test users and administrative accounts.
8. Document the setup with screenshots and command notes.
9. Validate the Windows Server/Ubuntu mixed environment.
10. Take a snapshot after the clean AD baseline is working.

## Later Security Roadmap

After Active Directory is complete, the lab will move toward a more security-focused design:

1. Cross-platform validation between Windows Server, Ubuntu Server, and clients.
2. Windows client VM and domain join.
3. Group Policy basics.
4. OPNsense firewall introduction.
5. Migration of lab VMs behind OPNsense-controlled networks.
6. Monitoring/logging with Windows and Linux sources.
7. Backup and restore testing.
8. Security detection and incident-style documentation.
