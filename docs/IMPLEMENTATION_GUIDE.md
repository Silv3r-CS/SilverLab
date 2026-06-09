# Implementation Guide: First GitHub Contribution

This guide explains how to upload the first SilverLab homelab contribution to GitHub.

## 1. Create the GitHub repository

Create a new GitHub repository named:

```text
silverlab-homelab
```

Recommended settings:

```text
Visibility: Public
Add README: No
Add .gitignore: No
License: Optional
```

This package already includes the README and documentation files.

## 2. Extract the ZIP

Extract the ZIP file on your computer.

You should see:

```text
silverlab-first-github-contribution/
├── README.md
├── docs/
│   ├── 01-initial-lab-build.md
│   └── 02-troubleshooting-usb-lan-fix.md
└── assets/
    └── diagrams/
        └── current-topology.mmd
```

## 3. Upload the files to GitHub using the browser

Open your new GitHub repository.

Click:

```text
Add file → Upload files
```

Drag and drop the contents of the extracted folder into GitHub.

Make sure the repository root contains:

```text
README.md
docs/
assets/
```

Do not upload the parent folder itself if GitHub creates an extra unnecessary layer.

Correct:

```text
silverlab-homelab/README.md
silverlab-homelab/docs/01-initial-lab-build.md
```

Incorrect:

```text
silverlab-homelab/silverlab-first-github-contribution/README.md
```

## 4. Use this commit message

```text
Initial SilverLab homelab documentation
```

Description:

```text
Document initial Proxmox setup, SilverLab network topology, USB-to-LAN adapter fix, and planned next steps.
```

## 5. What to add next

After creating the Ubuntu VM, add a new file:

```text
docs/03-ubuntu-admin-vm.md
```

Include:

```text
VM settings
Installation steps
IP address
Network tests
Screenshots
Problems encountered
Lessons learned
```

## 6. Screenshots to add later

Create:

```text
assets/screenshots/
```

Then add screenshots such as:

```text
proxmox-dashboard.png
proxmox-storage-layout.png
proxmox-network-vmbr0.png
silverlab-router-wifi.png
ubuntu-admin-vm-summary.png
```

Before uploading screenshots, remove or blur:

```text
Passwords
Public IP addresses
Serial numbers
Private keys
Personal browser tabs
```

## 7. Job-focused update style

Each future update should follow this pattern:

```text
Problem
Investigation
Fix
Result
Skills demonstrated
```

This makes the repository useful for job applications and interviews.
