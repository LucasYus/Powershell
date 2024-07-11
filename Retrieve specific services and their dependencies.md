# Retrieve Specific Services and Their Dependencies

## Explanation by parts

## Retrieve Specific Services:
```
Get-WmiObject -Class win32_service | where {($_.name -eq "Audiosrv") -or ($_.name -eq "CryptSvc")}

```
Retrieves details of the Windows services named Audiosrv (Windows Audio) and CryptSvc (Cryptographic Services) using Get-WmiObject with the win32_service class.

## Foreach Loop to Process Required Services:
```
foreach($servicio in (Get-Service -Name Audiosrv).RequiredServices)
```
Iterates through each service that is required by the Audiosrv service.

## Retrieve Process ID of Each Required Service:
```
(Get-WmiObject -Class win32_service | where name -EQ $servicio.name | select *).processid
```
For each required service ($servicio), retrieves its details using Get-WmiObject with the win32_service class.

# All the code
```
Get-WmiObject -Class win32_service | where {($_.name -eq "Audiosrv") -or ($_.name -eq "CryptSvc")}

foreach($servicio in (Get-Service -Name Audiosrv).RequiredServices)
{
    (Get-WmiObject -Class win32_service | where name -EQ $servicio.name | select *).processid
}
```
