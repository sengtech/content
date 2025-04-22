# MDI - Deployment guide

<br>

## Prerequisites

### ➡️ Portal permissions

- You need at least **Security administrator** access on your tenant to access the Identity section of the Microsoft Defender XDR Settings area and create the workspace.
- For more information, see [Microsoft Defender for Identity role groups](https://learn.microsoft.com/en-us/defender-for-identity/role-groups).

### ➡️ AD Permissions

- Domain Admin

### ➡️ Licensing requirements

- [Link](https://learn.microsoft.com/en-us/defender-for-identity/deploy/prerequisites#licensing-requirements)
- Enterprise Mobility + Security E5 (EMS E5/A5)
- Microsoft 365 E5 (Microsoft E5/A5/G5)
- Microsoft 365 E5/A5/G5/F5 Security
- Microsoft 365 F5 Security + Compliance
- A standalone Defender for Identity license

### ➡️ Sensor requirements and recommendations

- [Link](https://learn.microsoft.com/en-us/defender-for-identity/deploy/prerequisites#sensor-requirements-and-recommendations)

### ➡️ Networking

- [Link](https://learn.microsoft.com/en-us/defender-for-identity/deploy/prerequisites#required-ports)
- Verify that the servers you intend to install Defender for Identity sensors on can reach the Defender for Identity cloud service. From each server, try accessing: `https://*your-workspace-name*sensorapi.atp.azure.com`

<br>

## Consideration

- Multiple forrests, domains et.c.


<br>

## Deployment steps

### ➡️ Tools

**Test MDI Readiness**

- [Test-MdiReadiness.ps1](https://github.com/microsoft/Microsoft-Defender-for-Identity/tree/main/Test-MdiReadiness)

**PowerShell module**

- [DefenderForIdentity module documentation](https://learn.microsoft.com/en-us/powershell/module/defenderforidentity/?view=defenderforidentity-latest)
- [Introducing the new PowerShell Module for Microsoft Defender for Identity](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/introducing-the-new-powershell-module-for-microsoft-defender-for-identity/4028734)
- [Defender for Identity PowerShell module update](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/defender-for-identity-powershell-module-update/4208525)

### ➡️ Sensor installation

The MDI sensor needs to be installed on all

- ✅ Domain Controllers
- ✅ Active Directory Certificate Services (AD CS)
- ✅ Active Directory Federation Services (AD FS)
- ✅ Entra Connect

### ➡️ MDI “New” Sensor

- [Activate Microsoft Defender for Identity capabilities directly on a domain controller](https://learn.microsoft.com/en-us/defender-for-identity/deploy/activate-capabilities)

<br>

## Post-Deployment steps

### ➡️ Configure Windows event collection

- The preferred way is through the PowerShell module
- [Configure audit policies for Windows event logs](https://learn.microsoft.com/en-us/defender-for-identity/deploy/configure-windows-event-collection)

### ➡️ Configure a Directory Service account (DSA) for use with Defender for Identity (gMSA)

- The preferred way is through the PowerShell module
- [Directory Service Accounts for Microsoft Defender for Identity](https://learn.microsoft.com/en-us/defender-for-identity/deploy/directory-service-accounts)
- [Configure a Directory Service Account for Defender for Identity with a gMSA](https://learn.microsoft.com/en-us/defender-for-identity/deploy/create-directory-service-account-gmsa)
- [Login as a service](https://learn.microsoft.com/en-us/defender-for-identity/deploy/create-directory-service-account-gmsa#verify-that-the-gmsa-account-has-the-required-rights)

<br>

> [!IMPORTANT]
> **Group:** `mdiSvcGroup01` <br>
> For anything beyond Domain Controllers - add these servers to this group

<br>

### ➡️ Configure SAM-R

- [Configure SAM-R to enable lateral movement path detection in Microsoft Defender for Identity](https://learn.microsoft.com/en-us/defender-for-identity/deploy/remote-calls-sam)
- Microsoft Defender for Identity mapping for potential lateral movement paths relies on queries that identify local admins on specific machines. These queries are performed with the SAM-R protocol, using the Defender for Identity Directory Service account you configured.

### ➡️ Configure Network Name Resolution

- Using NNR, Defender for Identity can correlate between raw activities (containing IP addresses), and the relevant computers involved in each activity. Based on the raw activities, Defender for Identity profiles entities, including computers, and generates security alerts for suspicious activities.
- [Network Name Resolution in Microsoft Defender for Identity](https://learn.microsoft.com/en-us/defender-for-identity/nnr-policy)

### ➡️ Configure Defender for Identity automated response exclusions

- [Configure Defender for Identity automated response exclusions](https://learn.microsoft.com/en-us/defender-for-identity/automated-response-exclusions)

### ➡️ Configure Microsoft Defender for Identity action accounts

- Using a dedicated gMSA as an action account is ***optional***
- [Instructions](https://learn.microsoft.com/en-us/defender-for-identity/deploy/manage-action-accounts)

### ➡️ Automated Response Exclusions

- [Configure Defender for Identity automated response exclusions](https://learn.microsoft.com/en-us/defender-for-identity/automated-response-exclusions)

### ➡️ Entity Tags
- [Defender for Identity entity tags in Microsoft Defender XDR](https://learn.microsoft.com/en-us/defender-for-identity/entity-tags#honeytoken-tags)

<br>

## Other

### ➡️ AD Recycle bin
Grayed out if already enabled (Active Directory Admin Center): <br>
<img src="https://github.com/user-attachments/assets/ab18ddd0-a5aa-430d-a5d1-d06c4c0a16ce" alt="CS_2025-03-24_1507" width="300" />


**Check if enabled in AD**
```
Get-ADOptionalFeature -Filter 'Name -like "*Recycle Bin*"' | Select-Object Name,EnabledScopes 
```
**EnabledScopes responses**
| Value | Status |
| ------------- | ------------- |
| { } | Not yet enabled (cannot disable) |
| {CN=NTDS Settings,CN=DC,CN=Servers,CN=MSSEC-SITE,CN=Sites,CN=Configuration,DC=mssec,DC=se} | Enabled |

