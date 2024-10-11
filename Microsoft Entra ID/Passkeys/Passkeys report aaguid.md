
## Entra ID Roles
```Global Reader + OAuth persmissions```

## Install module
```
Install-Module Microsoft.Graph.Identity.SignIns

Import-Module Microsoft.Graph.Identity.SignIns
```

## Don't try to use azcli login method unless GA
```
Disconnect-MgGraph
```

## Connect
```
Connect-MgGraph -UseDeviceCode -Scope AuditLog.Read.All, UserAuthenticationMethod.Read.All -NoWelcome
```

## AAGUIDs
```
((Get-MgReportAuthenticationMethodUserRegistrationDetail -Filter "methodsRegistered/any(i:i eq 'passKeyDeviceBound')" -All).Id | ForEach-Object { Get-MgUserAuthenticationFido2Method -UserId $_ -All }).AaGuid | Select-Object -Unique
```


