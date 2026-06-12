# Command Reference

This command reference records important Linux/Proxmox commands used during the SilverLab build. The goal is to show not just which commands were used, but why they were used.

## Network validation commands

### `ip -br a`

Shows network interfaces and IP addresses in a short readable format.

Used to confirm:

- Which interface is up
- Which IP address is assigned
- Whether Ubuntu received the reserved address
- Whether Proxmox was on the expected subnet

Example expected result for Ubuntu:

```text
ens18 UP 192.168.1.120/24
```

### `ip route`

Shows the routing table.

Used to confirm:

- Default gateway
- Whether traffic should go through the lab router
- Whether VPN/Tailscale routes are present when troubleshooting remote access

### `ping -c 4 192.168.1.1`

Sends four test packets to the lab router gateway.

Used to confirm basic local network connectivity.

### `ping -c 4 8.8.8.8`

Tests internet reachability by IP address.

Useful because it tests routing without relying on DNS.

### `ping -c 4 google.com`

Tests both internet reachability and DNS resolution.

If ping to `8.8.8.8` works but `google.com` fails, DNS is likely the problem.

## Proxmox commands

### `cat /etc/network/interfaces`

Displays the Proxmox network configuration file.

Used to confirm:

- Proxmox static IP
- Gateway
- Bridge configuration
- Which physical interface is attached to `vmbr0`

### `systemctl status pveproxy --no-pager`

Checks the Proxmox web proxy service.

Used to confirm whether the Proxmox web UI service is running.

### `ss -lntp | grep 8006`

Checks whether a service is listening on TCP port `8006`, the Proxmox web interface port.

Used to confirm that Proxmox was accepting local web management connections.

### `reboot`

Restarts the system.

Used after network configuration changes when a clean reload was the safest way to apply changes.

## Ubuntu Server commands

### `sudo apt update`

Refreshes the package list from configured repositories.

Used before installing packages so Ubuntu knows the latest available versions.

### `sudo apt install <package>`

Installs software packages.

Used to install admin tools and QEMU Guest Agent.

### `hostnamectl`

Shows system identity and OS details.

Used to document the Ubuntu baseline: hostname, OS version, kernel, architecture, and virtualization environment.

### `df -h`

Shows filesystem usage in human-readable units.

Used to confirm disk usage and available space.

### `free -h`

Shows memory and swap usage in human-readable units.

Used to confirm that the 2 GB Ubuntu VM has enough available memory for the current role.

### `uptime`

Shows how long the server has been running, number of users, and load average.

Used as a quick system health check.

### `systemctl status qemu-guest-agent --no-pager`

Checks whether QEMU Guest Agent is running.

The `--no-pager` option prints output directly in the terminal instead of opening a scrollable pager. This is useful for screenshots and documentation.

### `ssh user@192.168.1.120`

Connects to the Ubuntu Server VM over SSH.

Used to confirm remote administration from Laptop 1.

## Remote access/troubleshooting commands

### `tailscale status`

Shows Tailscale devices and connection state.

Used to confirm that the Proxmox host and admin device were connected to the private Tailscale network.

### `nc -vz <host> 8006`

Tests whether TCP port `8006` is reachable.

Used to check whether the Proxmox web interface could be reached over the network.

### `curl -k https://<host>:8006`

Tests whether Proxmox responds over HTTPS.

The `-k` option allows curl to connect despite Proxmox using a self-signed certificate.

### `tcpdump`

Captures network packets.

Used during deeper troubleshooting to confirm whether traffic was actually reaching the Proxmox host.

## Documentation rule

Commands should be documented when they show one of these things:

1. A configuration decision
2. A troubleshooting step
3. A validation result
4. A repeatable admin process
5. A skill relevant to IT support, infrastructure, or cyber roles
