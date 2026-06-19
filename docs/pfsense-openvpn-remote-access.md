# pfSense and OpenVPN Remote Access

This milestone documents pfSense firewalling, DNS/DHCP design, and OpenVPN remote-access validation for SilverLab.

## Objective

Provide a protected lab network behind pfSense and validate secure remote access into that network from an external client scenario.

## pfSense Role

**SILVER-FW01** runs pfSense CE and provides:

- Firewalling between the home/management side and the protected SilverLab LAN.
- LAN gateway at `192.168.1.1`.
- DHCP for SilverLab clients.
- DNS Resolver for clients.
- Domain override forwarding for `silverlab.local` to SILVER-DC01.
- OpenVPN remote access.

## Network Placement

| Interface | Network | Role |
|---|---|---|
| WAN | Home / management side | Upstream connection through the home router. |
| LAN | Protected SilverLab LAN | Gateway for internal lab devices and VMs. |

## DNS Behaviour

Clients use pfSense as DNS at `192.168.1.1`. pfSense forwards queries for `silverlab.local` to the domain controller at `192.168.1.10`.

This provides internal AD/DNS functionality while keeping general client DNS simple and resilient.

## OpenVPN Validation

OpenVPN was validated from **SILVER-CLIENT01** while the client was not directly connected to the SilverLab LAN. The wired SilverLab connection was disabled and the client used an external/mobile-hotspot path.

Validation outcome:

| Test area | Result |
|---|---|
| VPN profile loads | Passed |
| VPN user authentication | Passed |
| Tunnel assignment | Passed; client received a `10.8.9.x` tunnel address |
| pfSense LAN reachability | Passed |
| Internal DC/domain reachability | Passed during validation |
| `silverlab.local` DNS path | Passed during validation |

## Security Notes

The following should not be published in the repository:

- Public IP address
- VPN exported `.ovpn` files
- Certificates or private keys
- pfSense configuration backups
- VPN usernames/passwords
- Full OpenVPN logs if they reveal endpoints, usernames, certificate names, or public IP information

## Evidence Captured

Recommended screenshots:

| Screenshot | Purpose |
|---|---|
| OpenVPN connected notification | Shows external-client tunnel establishment. |
| pfSense OpenVPN status page | Shows server-side VPN session, after redaction. |
| Client validation output | Shows internal resource reachability, after redaction where required. |

## Portfolio Skills Demonstrated

- Firewall/router deployment
- Split network design
- DHCP and DNS forwarding
- Remote-access VPN setup
- External-client validation
- Secure documentation and redaction practice
