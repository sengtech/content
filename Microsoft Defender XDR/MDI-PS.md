# MDI PowerShell Module

[Reference Microsoft Learn](https://learn.microsoft.com/en-us/powershell/defenderforidentity/overview-defenderforidentity?view=defenderforidentity-latest)

## 📦 Install module
```
Install-Module -Name DefenderForIdentity
Import-Module -Name GroupPolicy -SkipEditionCheck
```


## 👤 Create Directory Service Accounts (DSA) using gMSA 

### Create account
```
New-MDIDSA -Identity “mdiSvc01” -GmsaGroupName “gMSA-MDI-Group” -Verbose
```

<br>

> [!NOTE]
> If you plan on using Active Directory Federation Services (ADFS) or Active Directory Certificate Services (ADCS), the security group created in the previous step will need to include the ADFS and/or ADCS servers.

<br>

### Test account
```
Test-MDIDSA -Identity "mdiSvc01" -Detailed
```
<br>

## ⚙️ MDI Configuration

### Create configuration
```
Set-MDIConfiguration -Mode Domain -Configuration All -Identity mdiSvc01 -verbose
```

### Test configuration
```
Test-MDIConfiguration -Mode Domain -Identity gMSA-MDI -Configuration All -Verbose
```

### Configuration report
```
New-MDIConfigurationReport -Path C:\temp -OpenHtmlReport
```
