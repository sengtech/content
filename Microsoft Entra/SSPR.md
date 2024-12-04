# 🔑 SSPR

### 💡Why?

Microsoft Entra self-service password reset (SSPR) lets users reset their passwords in the cloud. Password changes for synced users can be written back to on-preminses AD using Password Writeback.

### ✅ Prerequisites

- At least Microsoft Entra ID P1 (synced users or writeback)
- At least Hybrid Identity Administrator / Authentication Policy Administrator

### 🚶‍♂️Steps

For hybrid deployment

1. Enable SSPR in Microsoft Entra ID
2. Enable password writeback in Microsoft Entra Connect Sync
3. Enable password writeback in Microsoft Entra ID
4. Set minimum password age policy
    1. The group policy for Minimum password age must be set to 0 for password writeback to work most efficiently.
    2. Browse to Default Domain Policy > Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy.

### 🤔 Considerations

- Is the Authencation Methods migration completed?

### 🚪End user portals

[aka.ms/sspr](https://aka.ms/sspr)

[aka.ms/mysecurityinfo](https://aka.ms/mysecurityinfo)

### 🔐 What authentication methods are available for SSPR?

[How each authentication method works](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-methods#how-each-authentication-method-works)

### 🤔 Servicedesk considerations

- Password hash synchronization back to Microsoft Entra ID is scheduled for every 2 minutes
- Users need to register, using the right method

### 🔀 Administrator reset policy differences

By default, administrator accounts are enabled for self-service password reset, and a strong default two-gate password reset policy is enforced. Administrators with sensitive roles should use phishing-resistant authentication methods only and therefore ***not*** able to reset their password using SSPR.
[Link](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-sspr-policy#administrator-reset-policy-differences) 

### 🔗 Links

[Tutorial: Enable users to unlock their account or reset passwords using Microsoft Entra self-service password reset](https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-enable-sspr)

[Self-service password reset rollout materials](https://www.microsoft.com/en-us/download/details.aspx?id=56768)

---

## 🔄 Password Writeback

Password writeback allows password changes in the cloud to be written back to an on-premises directory in real time by using either Microsoft Entra Connect or Microsoft Entra Connect cloud sync.

Supported in environments that use the following hybrid identity models

- [Password hash synchronization](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-password-hash-synchronization)
- [Pass-through authentication](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-pta)
- [Active Directory Federation Services](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-fed-management)

### 🔎 Pre-check

Is Password-writeback enabled?

`Entra Admin Center → Protection → Password reset → On-premises integration`

### 🔦 Highlights

- Supports password writeback when an admin resets them from the Microsoft Entra admin center
    - For federated or PHS

### 🔗 Links

[How does self-service password reset writeback work in Microsoft Entra ID?](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-sspr-writeback)

[Tutorial: Enable Microsoft Entra self-service password reset writeback to an on-premises environment](https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-enable-sspr-writeback)
