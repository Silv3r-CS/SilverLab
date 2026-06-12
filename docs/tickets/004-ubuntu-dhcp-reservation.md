# Ticket 004 - Ubuntu DHCP Reservation Validation

| Field | Detail |
|---|---|
| Type | Configuration validation |
| Impact | Ensures Ubuntu Server VM has a stable address for SSH and future services |
| Priority | Medium |

## Issue

The Ubuntu Server VM needed a consistent address for SSH, future Nginx service hosting, firewall rules, and documentation.

## Configuration

A DHCP reservation was created on the TP-Link Archer C6 router for the Ubuntu VM.

Reserved address:

```text
192.168.1.120
```

## Validation command

```bash
ip -br a
```

## Expected result

The Ubuntu VM interface should show:

```text
ens18 UP 192.168.1.120/24
```

## Outcome

The Ubuntu VM successfully received the reserved IP address.

## Skills demonstrated

- DHCP reservation
- Network validation
- Linux command-line checks
- Stable service address planning
