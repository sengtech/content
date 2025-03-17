# ADFS Decomission

## Prerequisites

### Required roles

- Manage federation settings - Global Administrator + Graph Powershell permission `"Domain.ReadWrite.All", "Directory.AccessAsUser.All”`
- Staged rollout - Hybrid Identity Administrator

## Things to consider

- Organization branding
- Device enrollment ⚠️
- Applications may use a federated protocol that is not available in Entra (Shibboleth) - [Link](https://dirteam.com/sander/2025/03/17/from-the-field-three-gotchas-when-migrating-applications-from-ad-fs-to-entra/)
- Applications may use an outdated attribute for Name ID (userPrincipalName/sAMAccountName)  - [Link](https://dirteam.com/sander/2025/03/17/from-the-field-three-gotchas-when-migrating-applications-from-ad-fs-to-entra/)
- User assignment does not support group nesting  - [Link](https://dirteam.com/sander/2025/03/17/from-the-field-three-gotchas-when-migrating-applications-from-ad-fs-to-entra/)

### Logon Hours

- Not available at the moment in Entra ID. Possibly a future Conditional Access feature.

### Account expiration

- Possible with custom automation (e.g. scheduled task with Powershell)
- Do we need to review existing AD accounts with accounts expiration?

### Password expiration

- If a user is in the scope of password hash synchronization, by default the cloud account password is set to Never Expire.
- You can continue to sign in to your cloud services by using a synchronized password that is expired in your on-premises environment. Your cloud password is updated the next time you change the password in the on-premises environment.

[Link](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-password-hash-synchronization#password-expiration-policy)

### Account Lockout

- Entra ID Protection
- Smart Lockout - [Link](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-smart-lockout)

## Staged rollout

A great way to selectively test groups of users with cloud authentication capabilities like Microsoft Entra multifactor authentication, Conditional Access, Microsoft Entra ID Protection for leaked credentials, Identity Governance, and others, before cutting over your domains.

## Document current federation settings

`Get-MgDomainFederationConfiguration -DomainID yourdomain.com`

## Employee communication

- The user sign-in experience for accessing Microsoft 365 and other resources that are authenticated through Microsoft Entra ID changes.

## Plan rollback

- Take screenshots of the existing configuration of your app
- Be aware of the apps that support multiple IdPs since they provide an easier rollback plan

## Switching sign-in method

### Option A - Using Microsoft Entra Connect

[Link](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/migrate-from-federation-to-cloud-authentication#option-a)

### Option B - Using Microsoft Entra Connect and PowerShell

[Link](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/migrate-from-federation-to-cloud-authentication#option-b)

## Complete your migration

- Test the new sign-in method
- Remove a user from staged rollout

## Decommission AD FS infrastructure
### High Level Steps

- Fully documented https://aka.ms/adfsdecom
- Take final backup
- Remove entries from load balancers/DNS
- Uninstall Remote Access role from WAP servers
- Uninstall ADFS role from ADFS servers
- Delete ADFS Database (WID/SQL)
- Delete ADFS Certificates
- Delete ADFS Service Account
- Delete certificate sharing container in Active Directory
- Retire/reformat server disks

## Notes
- When you migrate from federated to cloud authentication, the process to convert the domain from federated to managed may take up to 60 minutes. During this process, users might not be prompted for credentials for any new logins to Microsoft Entra admin center or other browser based applications protected with Microsoft Entra ID. We recommend that you include this delay in your maintenance window.
- Consider planning cutover of domains during off-business hours in case of rollback requirements.

## Notes from the field
- "Option A" from migration guide never changed the domain setting from "Federated" to "Managed". Instead got stuck and even froze the Entra Conenct sync process. Choose "Option B" instead, with configuring the Entra Connect sync option to "Do not configure", and swithching the domain mode to "Managed", by using Graph PowerShell

## Links and Resources

[Migrate from federation to cloud authentication](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/migrate-from-federation-to-cloud-authentication)

[Understand the stages of migrating application authentication from AD FS to Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migrate-adfs-apps-stages)

[ADFS migration guidelines | Migration phases](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migrate-adfs-apps-phases-overview)
