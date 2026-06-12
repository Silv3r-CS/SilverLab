# Ticket 005: Windows Server VirtIO Disk Driver During Installation

## Issue

During Windows Server installation, the installer did not initially show the 60 GiB Proxmox virtual disk.

## Impact

Windows Server could not continue installation until the virtual disk became visible.

## Cause

The VM was configured with a VirtIO SCSI disk/controller. Windows Server did not include the required VirtIO storage driver by default during setup.

## Resolution

The VirtIO ISO was attached to the VM and the VirtIO SCSI storage driver was loaded during Windows Setup using the `vioscsi` driver path. After loading the driver, the 60 GiB virtual disk became available for installation.

## Verification

Windows Server installation continued successfully after the disk appeared. The server later booted successfully, Remote Desktop was enabled, and the server was validated on the SilverLab network.

## Skills Demonstrated

- Windows Server installation troubleshooting
- Proxmox VirtIO driver awareness
- Virtual disk/controller troubleshooting
- Root-cause identification
- Technical documentation
