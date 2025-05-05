# MDI PowerShell Module

[Reference Microsoft Learn](https://learn.microsoft.com/en-us/powershell/defenderforidentity/overview-defenderforidentity?view=defenderforidentity-latest)

<br>

## 📦 Install module
```
Install-Module -Name DefenderForIdentity
Import-Module -Name GroupPolicy -SkipEditionCheck
```
<br>

## 👤 Create Directory Service Accounts (DSA) using gMSA 

### Create account
```
New-MDIDSA -Identity “mdiSvc01” -GmsaGroupName “gMSA-MDI-Group” -Verbose
```

<br>

> [!NOTE]
> - If you plan on using Active Directory Federation Services (ADFS) or Active Directory Certificate Services (ADCS), the security group created in the previous step will need to include the ADFS and/or ADCS servers.
> - [Login in as a service](https://learn.microsoft.com/en-us/defender-for-identity/deploy/create-directory-service-account-gmsa#verify-that-the-gmsa-account-has-the-required-rights)
> - If you use the Group Policy Management Editor to configure the Log on as a service setting, make sure you add both ```NT Service\All Services``` and the ```gMSA account``` you created.
> - Example Scenario: Suppose you set a policy in ⁠secpol.msc on a server, but a different policy is applied via a GPO at the domain level. The GPO will take precedence. If you run ⁠rsop.msc, you’ll see the domain GPO setting as the effective policy, not the local one.

<br>

### Test account
```
Test-MDIDSA -Identity "mdiSvc01" -Detailed
```
<br>

## ⚙️ MDI Configuration

### Create configuration
```
Set-MDIConfiguration -Mode Domain -Configuration All -Identity mdiSvc01 -Verbose
```

### Test configuration
```
Test-MDIConfiguration -Mode Domain -Identity mdiSvc01 -Configuration All -Verbose
Test-MDIConfiguration -Mode Domain -Identity mdiSvc01 -Configuration All -GpoNamePrefix "MDI" -Verbose
```

### Configuration report
```
New-MDIConfigurationReport -Path C:\temp -OpenHtmlReport
```
