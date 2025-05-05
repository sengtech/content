# MDI PowerShell Module

## 👤 Create Directory Service Accounts (DSA) using gMSA 

### Create account
```
New-MDIDSA -Identity “gMSA-MDI” -GmsaGroupName “gMSA-MDI-Group” -Verbose
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
Set-MDIConfiguration -Mode Domain -Configuration All -Identity gMSA-MDI -verbose
```
