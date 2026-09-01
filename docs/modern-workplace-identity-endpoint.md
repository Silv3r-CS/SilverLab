# Modern Workplace: Identity and Endpoint Management

## Purpose

This workstream extends SilverLab beyond on-premises Active Directory into Microsoft Modern Workplace administration. The goal is to practise the support and administration tasks commonly seen in IT Support, Service Desk, Desktop/EUC and junior Modern Workplace roles.

This is an independent lab environment used for practical learning and validation. It is not presented as production or paid Microsoft 365 administration experience.

## Environment

- Windows 11 client virtual machines
- Windows Server Active Directory Domain Services and DNS
- Microsoft Entra ID
- Microsoft Entra Connect hybrid identity synchronisation
- Microsoft Intune
- Windows Autopilot practice
- Entra security groups and group-targeted assignments
- MFA testing
- Jira-based task and troubleshooting documentation

## Implemented and Validated

### Hybrid identity

- Connected the on-premises `silverlab.local` Active Directory environment to Microsoft Entra ID using Entra Connect.
- Validated synchronisation between local directory objects and Entra ID.
- Used users and security groups to test identity and access assignments.

### Intune enrolment and device management

- Prepared Windows 11 clients for cloud management, including disconnecting a test client from the on-premises domain where a clean enrolment scenario was required.
- Enrolled Windows devices into Intune and validated device visibility and assignment behaviour from both the admin portal and the endpoint.
- Tested MDM scope and group-based targeting rather than relying only on tenant-wide assignments.
- Practised Windows Autopilot workflows and endpoint validation.

### Access and sign-in policy troubleshooting

A practical troubleshooting scenario involved a Windows sign-in restriction that did not initially behave as expected.

- Verified the user and security-group relationship.
- Checked the identifier used for policy targeting and corrected an incorrect SID target.
- Triggered policy/device synchronisation and re-tested the endpoint.
- Confirmed the expected sign-in restriction after the corrected assignment was applied.
- Re-tested after group membership changes to understand policy propagation and endpoint refresh behaviour.

The value of this exercise was not simply applying a policy; it required separating group membership, identity translation, cloud assignment and endpoint synchronisation as individual troubleshooting layers.

### Authentication and security

- Practised MFA configuration and validation with test users.
- Used group-based assignments so policies could be tested against controlled user populations.
- Evaluated when endpoint/device restrictions are appropriate and when identity-based controls such as Conditional Access are a better design choice.

## Support Skills Demonstrated

| Area | Practical evidence |
|---|---|
| Windows support | Windows 11 enrolment, sign-in validation, domain join/disconnect and endpoint troubleshooting |
| Identity | Active Directory, Entra ID, Entra Connect, users, groups and hybrid synchronisation |
| Endpoint management | Intune enrolment, MDM scope, group-targeted assignments and policy synchronisation |
| Deployment | Windows Autopilot practice and endpoint validation |
| Security | MFA testing, controlled group assignment and access-policy evaluation |
| Troubleshooting | SID/identity targeting, policy propagation, group membership and expected-versus-actual testing |
| Documentation | Jira-based task tracking, validation notes and repeatable troubleshooting evidence |

## Working Method

For each change, the lab process is to:

1. Define the expected result.
2. Make one controlled configuration change.
3. Synchronise or refresh the affected service/endpoint when required.
4. Test with the intended user or device.
5. Record the actual result.
6. Troubleshoot differences rather than assuming the policy has applied.
7. Re-test after correction.

This approach is intended to demonstrate the support mindset behind the technology: clear scope, controlled changes, validation, evidence and handover-ready documentation.

## Next Development

The Modern Workplace workstream continues to expand through structured SilverLab tasks, with future evidence focused on endpoint compliance, identity-based access control, support workflows and administration scenarios that remain relevant to entry-level Microsoft support roles.
