# Secure Remote Access with Tailscale

This document records the secure remote access model used in SilverLab.

## Objective

Provide remote access to the Proxmox management interface without exposing Proxmox directly to the public internet.

## Design decision

SilverLab uses Tailscale for private remote access. Proxmox is not publicly port-forwarded.

```text
Recommended: Tailscale private access
Avoided: Public port forwarding to Proxmox
```

## Why this matters

Proxmox is an administrative control plane. Exposing it directly to the public internet would create unnecessary risk. Tailscale provides private connectivity between trusted devices instead.

## Current model

| Area | Approach |
|---|---|
| Local Proxmox access | `https://192.168.1.200:8006` |
| Remote Proxmox access | Tailscale private network |
| Public port forwarding | Not used |
| Ubuntu direct Tailscale access | Not currently required |
| Current preferred workflow | Tailscale to Proxmox, then Proxmox console/SSH as needed |

## Troubleshooting experience

During earlier remote-access testing, route and connectivity checks were used to confirm whether traffic was going over the correct interface and whether Proxmox was receiving traffic. This demonstrated useful real-world troubleshooting skills but detailed Tailscale identifiers are intentionally excluded from this public documentation.

Useful validation commands included:

| Command | Purpose |
|---|---|
| `tailscale status` | Check Tailscale device state |
| `ip route` | Confirm route selection |
| `nc -vz <host> 8006` | Test whether Proxmox web port is reachable |
| `curl -k https://<host>:8006` | Test HTTPS response from Proxmox |
| `tcpdump` | Confirm whether packets reached the Proxmox host |

## Outcome

Remote Proxmox access was restored and validated through the private Tailscale network after router migration.

## Security note

This document intentionally excludes Tailscale user/tailnet identifiers and private Tailscale device addresses. The important transferable skill is the access model: secure private remote access without public exposure.
