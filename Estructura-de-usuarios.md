## To start with the users section, we will create 2 files on the desktop where we will save the group name and the user.
## Then, we will use a foreach loop to create an OU, add the group, create the user, and add the user to the group.

```
function organizativa ()
{
    cd C:\Users\Administrator\Desktop
    ###Grupos y Usuarios
    "Sistemas" | out-file C:\Users\Administrator\Desktop\grupos.txt
    "Lucas" | out-file  C:\Users\Administrator\Desktop\usuarios.txt

    ###Unidad Orgalizativa
    $ou= New-ADOrganizationalUnit -DisplayName "Clases" -Name "Clases" -Path "dc=insti,dc=loc"

    foreach($grupo in Get-Content .\grupos.txt)
    {
        $grupo.split(",")
        New-ADGroup -Name $grupo -samAccountName $grupo -GroupScope DomainLocal -DisplayName $grupo -path "OU=Clases,DC=insti,DC=loc"
    }
 
    foreach($usuario in Get-Content .\usuarios.txt)
    {
        $usuario
        $password= (ConvertTo-SecureString "Alum4dos" -AsPlainText -Force)
        if(Get-ADUser -LDAPFilter "(samaccountname=$usuario)")
        {
        "El usuario $usuario ya existe"
        }
        else
        {
            New-ADUser -Name $usuario -SamAccountName $usuario -Path "OU=Clases,DC=insti,DC=loc" -AccountPassword $password -Enable $true
            Add-ADGroupMember "Sistemas" Lucas
        }
 }
}

```