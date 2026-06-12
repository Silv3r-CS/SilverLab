# Ubuntu Server Baseline

This document records the baseline deployment of the first Ubuntu Server VM in SilverLab.

## Objective

Create a lightweight Linux server VM on Proxmox that can be used for administration practice, service deployment, SSH, firewalling, web services, monitoring, and future log forwarding.

## VM baseline

| Item | Value |
|---|---|
| VM name | `SilverServer-Ubuntu` |
| Hostname | `homelab-silver` |
| Role | Linux server baseline |
| vCPU | 2 cores |
| RAM | 2 GB |
| Disk | 32 GB virtual disk |
| Network | VirtIO NIC on `vmbr0` |
| IP address | `192.168.1.120` |
| Access method | SSH from Laptop 1 |

## Installed baseline tools

The Ubuntu VM was built with SSH enabled and a practical admin toolkit.

```text
curl
wget
git
net-tools
dnsutils
traceroute
nmap
htop
qemu-guest-agent
```

A reference list is stored in:

[`../configs/ubuntu-baseline-packages.txt`](../configs/ubuntu-baseline-packages.txt)

## Important validation commands

| Command | Purpose | Why it was used |
|---|---|---|
| `hostnamectl` | Show hostname, OS, kernel, and virtualization information | Confirms the VM identity and system baseline |
| `ip -br a` | Show network interfaces and IPs | Confirms the reserved address `192.168.1.120` is active |
| `df -h` | Show filesystem usage | Confirms available disk space |
| `free -h` | Show memory and swap usage | Confirms the VM is running comfortably within allocated RAM |
| `uptime` | Show uptime and load | Confirms recent reboot/availability and system load |
| `systemctl status qemu-guest-agent --no-pager` | Check guest agent state | Confirms Proxmox guest integration |
| `ssh user@192.168.1.120` | Remote shell access | Confirms Laptop 1 can administer the VM over the network |

## QEMU Guest Agent

QEMU Guest Agent was installed and validated. The service showed as active/running and Proxmox was able to communicate with the guest agent.

This matters because it improves VM management from Proxmox, including more accurate status reporting and cleaner guest operations.

## SSH validation

SSH access from Laptop 1 to the Ubuntu VM was successfully validated. This proves that the VM can be administered remotely inside the lab network.

## Outcome

The Ubuntu Server VM is stable and ready for the next service milestone:

```text
Nginx internal web service + UFW firewall baseline
```

## Skills demonstrated

- Linux VM deployment
- DHCP reservation validation
- SSH administration
- Baseline package installation
- Filesystem/memory/network checks
- Proxmox guest integration
- Documentation of commands and outcomes
