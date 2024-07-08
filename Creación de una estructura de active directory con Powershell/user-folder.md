## In this function, we perform the same actions as in the previous folder, but specifically grant access to the user, who will be the only one besides administrators with access to their folder.

```
function userfolder ()
{
    New-Item -Path "C:\export\Sistemas\Lucas" -ItemType Directory

# Ruta de la carpeta "Sistemas"
$SistemasPath = "C:\export\Sistemas"

# Obtener una lista de las carpetas dentro de "Sistemas"
$carpetasUsuarios = Get-ChildItem -Path $SistemasPath -Directory

# Obtener el objeto de seguridad de la carpeta "Sistemas"
$aclSistemas = Get-Acl -Path $SistemasPath

# Obtener el objeto de usuario del administrador local
$administrador = [System.Security.Principal.NTAccount]::new("BUILTIN\Administrators")

# Crear una regla de acceso para el administrador local con permisos existentes
$administradorRule = New-Object System.Security.AccessControl.FileSystemAccessRule($administrador, "FullControl", "ContainerInherit, ObjectInherit", "None", "Allow")

# Aplicar la regla de acceso al objeto de seguridad de "Sistemas"
$aclSistemas.AddAccessRule($administradorRule)

# Configurar permisos específicos para cada carpeta de usuario dentro de "Sistemas"
foreach ($carpetaUsuario in $carpetasUsuarios) {
    $usuario = $carpetaUsuario.Name
    $rutaCarpetaUsuario = Join-Path -Path $SistemasPath -ChildPath $usuario

    # Obtener el objeto de seguridad de la carpeta de usuario
    $aclUsuario = Get-Acl -Path $rutaCarpetaUsuario

    # Quitar herencia en la carpeta de usuario
    $aclUsuario.SetAccessRuleProtection($true, $false)

    # Crear una regla de acceso para dar control total al usuario y al administrador local
    $ruleUsuario = New-Object System.Security.AccessControl.FileSystemAccessRule("insti.loc\$usuario", "FullControl", "ContainerInherit, ObjectInherit", "None", "Allow")
    $aclUsuario.AddAccessRule($ruleUsuario)
    $aclUsuario.AddAccessRule($administradorRule)

    # Aplicar los permisos a la carpeta de usuario
    Set-Acl -Path $rutaCarpetaUsuario -AclObject $aclUsuario
}

# Aplicar los permisos en "Sistemas"
Set-Acl -Path $SistemasPath -AclObject $aclSistemas
}
```
