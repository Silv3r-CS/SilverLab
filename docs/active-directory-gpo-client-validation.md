# Active Directory, GPO, and Client Validation

This milestone documents the Windows Server and Active Directory portion of SilverLab.

## Objective

Build and validate a small-business style Microsoft identity environment using Windows Server, Active Directory, organisational units, groups, a domain-joined client, and Group Policy.

## Implemented Components

| Component | Status |
|---|---|
| Windows Server VM | Built in Proxmox |
| Server name | **SILVER-DC01** |
| Domain | `silverlab.local` |
| AD DS | Installed and promoted |
| DNS | Installed with AD DS and used for the internal domain |
| OU structure | Created |
| Baseline users/groups | Created |
| Windows client | **SILVER-CLIENT01** joined to domain |
| GPO validation | Completed |

## OU Structure

The baseline Active Directory structure includes:

```text
silverlab.local
└── SilverLab
    ├── Users
    ├── Admins
    ├── Computers
    ├── Groups
    └── Service Accounts
```

This structure separates normal users, administrative users, computer objects, security groups, and service accounts so that future policies and permissions can be applied cleanly.

## Client Validation

**SILVER-CLIENT01** was joined to the `silverlab.local` domain and then moved into:

```text
SilverLab -> Computers
```

This placement was required so the workstation baseline GPO could apply to the client from the correct OU.

## Group Policy Validation

A baseline workstation GPO was linked to the Computers OU.

Validation evidence:

- The client computer object was moved to the correct OU.
- Computer-scope Group Policy was refreshed.
- `gpresult` confirmed the workstation baseline GPO applied.
- A SilverLab logon banner appeared on the Windows client.

The logon banner is strong evidence because it confirms the GPO changed client behaviour, not just that the policy object exists.

## Evidence Captured

Recommended screenshots for this milestone:

| Screenshot | Purpose |
|---|---|
| ADUC OU structure | Shows the organised AD baseline. |
| Group membership | Shows baseline support/admin group planning, with personal names redacted. |
| Client object inside `SilverLab -> Computers` | Shows correct OU placement for policy. |
| GPO logon banner | Proves the workstation baseline policy applied. |

## Portfolio Skills Demonstrated

- Windows Server administration
- Active Directory Domain Services
- Organisational Unit design
- User and group management
- Group Policy linking and validation
- Domain-joined Windows client administration
- Evidence-based validation using `gpresult`
