## Práctica del tema: crear un formulario que permita introducir nombres y operación (crear usuario, grupo, OU, etc.) al departamento de Recursos Humanos, cada vez que se introduce un usuario se añade a un fichero JSON que se sube a un servidor web, por otro lado, desarrollar un script que lea ese fichero JSON desde una URL y realice las operaciones que están indicadas (crear usuario, grupo, OU, etc.) además para cada usuario crear un código QR

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
