# Enterprise Identity & Access Management Lab — Microsoft Entra ID

## Project Overview

This project simulates identity and access management (IAM) operations for a fictional company, **Northstar Technologies**, using Microsoft Entra ID.

The goal was to gain hands-on experience managing cloud-based user identities, configuring security groups, implementing role-based access control (RBAC), applying the principle of least privilege, and monitoring administrative activity.

The lab also included testing helpdesk permissions, verifying multifactor authentication (MFA), and reviewing security audit logs.

## Lab Environment

| Component | Description |
|---|---|
| Platform | Microsoft Entra ID |
| License | Microsoft Entra ID Free |
| Organization | Northstar Technologies (fictional) |
| User accounts | 7 |
| Security groups | 4 |
| Authentication | Microsoft Authenticator, Security Defaults |
| Monitoring | Microsoft Entra audit logs and sign-in logs |

## Project Objectives

- Create and manage cloud-based employee identities.
- Organize employees into departmental security groups.
- Configure administrative roles using RBAC.
- Identify and remediate excessive administrative privileges.
- Validate helpdesk permissions through practical testing.
- Review administrative audit logs.
- Verify MFA registration and authentication requirements.

## 1. User and Group Management

Configured an organizational environment containing six fictional employee accounts and one Global Administrator account.

Created four departmental security groups:

| Security Group | Department | Members |
|---|---|---|
| SG-Finance | Finance | Emma Chen, Olivia Martinez |
| SG-Human Resources | Human Resources | Daniel Kim, Sophia Patel |
| SG-IT | Information Technology | Alex Rivera |
| SG-Sales | Sales | Marcus Johnson |

These groups demonstrate how organizations can organize employee identities for centralized access management.

Group membership was configured manually using assigned membership. Resource-level permissions were not implemented as part of this lab.

## 2. Role-Based Access Control (RBAC)

Reviewed administrative role assignments and evaluated the security implications of excessive privileges.

### Security Finding: Excessive Administrative Privileges

During the lab, the IT support account belonging to Alex Rivera had Global Administrator privileges.

Global Administrator grants extensive administrative capabilities across Microsoft Entra ID and related services. This level of access was unnecessary for the fictional employee's helpdesk responsibilities.

### Remediation

Applied the principle of least privilege by:

1. Identifying the excessive Global Administrator assignment.
2. Removing Global Administrator privileges from Alex Rivera.
3. Assigning the built-in Helpdesk Administrator role.
4. Reviewing audit logs associated with the role changes.
5. Verifying that Alex retained only the Helpdesk Administrator directory role.

A final review of Global Administrator assignments confirmed that only the designated administrator account retained the role.

### Evidence

- [Excessive Global Administrator privileges](screenshots/01-excessive-global-admin-privilege.png)
- [Least-privilege remediation](screenshots/02-least-privilege-remediation.png)
- [Global Administrator removal audit log](screenshots/03-global-admin-removal-audit-log.png)
- [Helpdesk Administrator role assignment audit log](screenshots/04-helpdesk-role-assignment-audit-log.png)
- [Helpdesk role verification](screenshots/05-helpdesk-role-verification.png)

## 3. Helpdesk Permission Testing

Tested administrative permissions by signing in as Alex Rivera using the Helpdesk Administrator account.

### Scenario: Employee Password Reset

A fictional Finance employee, Emma Chen, required a password reset.

**Test procedure:**

1. Signed in using Alex Rivera's Helpdesk Administrator account.
2. Located Emma Chen in Microsoft Entra ID.
3. Initiated an administrative password reset.
4. Confirmed that the password reset completed successfully.

**Result:** Successful.

This demonstrated that the Helpdesk Administrator role permitted an authorized support operation without requiring Global Administrator privileges.

### Restricted Administrative Access

Verified that Alex Rivera held only the Helpdesk Administrator role, while Global Administrator privileges remained exclusively assigned to the designated administrator account.

According to Microsoft's role-based permission model, Helpdesk Administrators cannot reset Global Administrator passwords.

Additionally, an attempt to access organization-wide audit logs while signed in as Alex resulted in an access-denied error, demonstrating the restrictions associated with his assigned role.

### Evidence

- [Successful standard-user password reset](screenshots/06-standard-user-password-reset.png)
- [Global Administrator role verification](screenshots/07-privileged-account-role-verification.png)
- [Helpdesk audit log access denied](screenshots/08-helpdesk-audit-log-access-denied.png)

## 4. Audit Logging and Monitoring

Used Microsoft Entra audit logs to investigate the administrative password-reset operation.

Verified the following event details:

| Field | Recorded Value |
|---|---|
| Activity | Reset password (by admin) |
| Initiated by | Alex Rivera |
| Target | Emma Chen |
| Category | UserManagement |
| Status | Success |

The audit record confirmed who initiated the operation, which account was affected, and whether the action succeeded.

This exercise demonstrated how audit logs can support administrative accountability, security monitoring, and incident investigations.

### Evidence

- [Password reset audit activity](screenshots/09-password-reset-audit-activity.png)
- [Password reset audit target](screenshots/10-password-reset-audit-target.png)

## 5. Multifactor Authentication (MFA)

Reviewed Microsoft Entra authentication policies and confirmed that Security Defaults were enabled.

Security Defaults provide baseline identity protections, including MFA registration and authentication requirements.

### MFA Configuration Review

Verified that Microsoft Authenticator was enabled as an available authentication method.

Confirmed that Alex Rivera had registered Microsoft Authenticator, with notification-based authentication configured as his default MFA method.

### MFA Sign-in Testing

Performed a sign-in using Alex Rivera's test account.

During a fresh sign-in, Microsoft requested number matching through Microsoft Authenticator. The challenge was completed successfully.

Also reviewed a successful sign-in record showing that:

- Security Defaults was the applied authentication policy.
- The MFA requirement was recorded as satisfied.
- The authentication details indicated that the requirement had been previously satisfied for that recorded session.

A separate sign-in test successfully verified Microsoft Authenticator's number-matching functionality.

### Evidence

- [Security Defaults enabled](screenshots/11-security-defaults-enabled.png)
- [Microsoft Authenticator registration](screenshots/12-helpdesk-mfa-registration.png)
- [MFA sign-in verification](screenshots/13-mfa-signin-verification.png)

## 6. Project Limitations

This lab was completed using Microsoft Entra ID Free.

Certain premium functionality, including Conditional Access policy management and organization-wide authentication registration reporting, was unavailable.

The project therefore focused on supported capabilities such as Security Defaults, built-in administrative roles, user management, security groups, individual authentication-method reviews, and audit logging.

No production accounts or organizational resources were used.

## 7. Key Takeaways

Through this project, I gained practical experience with:

- **Identity management:** Creating and organizing cloud-based user accounts.
- **Access control:** Understanding the difference between departmental security groups and administrative roles.
- **Least privilege:** Identifying and reducing excessive administrative permissions.
- **Helpdesk administration:** Performing authorized password resets and validating role-based permissions.
- **Security monitoring:** Reviewing audit events to identify administrative actions and their outcomes.
- **Authentication security:** Configuring and validating MFA-related protections.

The project reinforced the importance of granting users only the permissions necessary for their responsibilities and verifying security configurations through hands-on testing.

## Tools & Technologies

- Microsoft Entra ID
- Microsoft Entra Admin Center
- Microsoft Authenticator
- Role-Based Access Control (RBAC)
- Security Groups
- Security Defaults
- Audit Logs
- Sign-in Logs

## Project Evidence

Supporting screenshots are organized in the `screenshots/` directory.

