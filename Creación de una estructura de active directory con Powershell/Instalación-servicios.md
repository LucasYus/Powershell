## In the first part of the project, we will install the Active Directory service along with the users and computers feature.
## To apply this change, we will have to reset our computer.

```

function Instalar ()
{
    ###Active directory
    Add-WindowsFeature AD-Domain-Services
    ###Usuarios Active directory
    Install-WindowsFeature -name AD-Domain-Services -IncludeManagementTools
    ###reset
    Restart-Computer
   
}

```
---

## After the restart for the first part, we install the forest for our domain and the DNS to complete the instalation.
## When we execute this command, a text box will appear and we will have to enter the domain administrator password.

```
function Forest ()
{
     ###Bosque y DNS
    Import-Module ADDSDeployment
    Install-ADDSForest
    -CreateDnsDelegation:$false
    -DatabasePath "c:\Windows\NTDS"
    -DomainMode "Win2012R2"
    -DomainName "Insti.loc"
    -DomainNetbiosName "PRUEBA"
     ForestMode "Win2012R2"
    -InstallDns:$true
    -LogPath "C:\Windows\NTDS"
    -NoRebootOnCompletion:$false
    -SysvolPath "C:\Windows\SYSVOL"
    -Force:$true
  
}
```
