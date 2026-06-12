# Windows Server VM Baseline

## Objective

Build and validate a Windows Server VM in Proxmox as the foundation for the next SilverLab milestone: Active Directory Domain Services.

This milestone demonstrates Windows Server installation, Proxmox VM planning, virtualisation-driver troubleshooting, Remote Desktop administration, and baseline network validation.

## Environment

| Component | Details |
|---|---|
| Proxmox VM | 101 - SilverWindowsServer25EVAL |
| Windows hostname | SILVER-DC01 |
| Operating system | Windows Server 2025 Standard Evaluation (Desktop Experience) |
| Hypervisor | Proxmox VE on Laptop 2 |
| VM firmware | OVMF / UEFI |
| Machine type | q35 |
| TPM | v2.0 enabled |
| CPU | 2 cores |
| Memory | 4 GiB |
| Disk | 60 GiB on `local-lvm` |
| Disk controller | VirtIO SCSI single |
| Network | VirtIO adapter on `vmbr0` |
| Current IPv4 address | 192.168.1.154 |
| Gateway | 192.168.1.1 |
| Remote access | Remote Desktop / RDP |

## Deployment Summary

A Windows Server VM was created on Proxmox with a modern virtual hardware profile using OVMF/UEFI, q35, TPM 2.0, VirtIO SCSI storage, and VirtIO networking. The server was installed with the Desktop Experience option to support Server Manager, GUI-based learning, screenshots, and future Active Directory administration.

After installation, Remote Desktop was enabled so the server can be managed from Laptop 1 instead of relying only on the Proxmox noVNC console.

## Installation Learning Points

### Correct guest OS type matters

During an earlier installation attempt, the VM OS type was accidentally left as Linux instead of Microsoft Windows. This caused incorrect VM defaults and contributed to boot/installation issues. The VM was recreated with the guest OS type set correctly to Microsoft Windows, after which the Windows Server installation proceeded successfully.

### VirtIO storage driver required

During Windows Server setup, the installer did not initially display the Proxmox virtual disk. This was expected because the VM used a VirtIO SCSI disk/controller for improved Proxmox performance, and Windows required the appropriate VirtIO storage driver before it could access the disk.

The driver was loaded from the attached VirtIO ISO using the `vioscsi` driver path. After loading the correct driver, the 60 GiB virtual disk became available for installation.

This was a useful learning point around Windows-on-Proxmox virtualisation drivers and practical installation troubleshooting.

## Key Configuration Choices

| Choice | Reason |
|---|---|
| Standard Evaluation | Suitable for learning Windows Server, AD DS, DNS, users, groups, and Group Policy basics |
| Desktop Experience | Easier for first Windows Server lab, screenshots, and GUI administration |
| 4 GiB RAM | Better baseline for a GUI Windows Server and future AD DS role |
| 2 CPU cores | Balanced allocation for an 8 GiB Proxmox host |
| 60 GiB disk | Provides enough room for Windows Server, updates, tools, and AD DS learning |
| OVMF / UEFI | Modern Windows-compatible firmware |
| q35 machine type | Modern VM chipset model |
| TPM 2.0 | Supports modern Windows security features and future BitLocker/security learning |
| VirtIO SCSI | Better Proxmox storage performance than legacy emulated controllers |
| VirtIO network on `vmbr0` | Places the server on the current SilverLab lab network |
| RDP enabled | Smoother administration from Laptop 1 than noVNC |

## Commands and Settings Used

### Enable Remote Desktop firewall rules

```powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
```

Purpose: enables inbound Windows Firewall rules for Remote Desktop.

### Enable Remote Desktop connections

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server" -Name "fDenyTSConnections" -Value 0
```

Purpose: changes the Windows registry setting so Remote Desktop connections are allowed.

### Validate hostname and network

```powershell
hostname
ipconfig
ping 192.168.1.1
ping 192.168.1.200
```

Purpose: confirms the server hostname, IP configuration, default gateway, and connectivity to the router and Proxmox host.

## Outcome

The Windows Server VM was installed successfully and renamed to:

```text
SILVER-DC01
```

The server received a lab network IP address:

```text
192.168.1.154
```

Remote Desktop access from Laptop 1 was successfully established, allowing the server to be managed over the SilverLab network instead of relying only on the Proxmox noVNC console.

## Evidence

| Screenshot | Purpose |
|---|---|
| `19-windows-server-vm-creation-summary-redacted.png` | Windows Server VM configuration summary in Proxmox |
| `20-windows-server-rdp-access-from-laptop1.png` | RDP access from Laptop 1 to Windows Server |
| `21-windows-server-hostname-network-baseline.png` | Hostname and network baseline validation |

## Skills Demonstrated

- Windows Server installation
- Proxmox Windows VM configuration
- VM resource planning on limited hardware
- VirtIO driver troubleshooting
- Windows Remote Desktop administration
- Windows Firewall rule validation
- Hostname and IP configuration checks
- Documentation of practical troubleshooting and successful outcomes

## Next Step

The next milestone is to install and configure Active Directory Domain Services. Before promotion to a Domain Controller, the server should receive a stable IP address or DHCP reservation so DNS and domain services remain predictable.
