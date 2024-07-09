## Monitor processor usage and display a notification if usage exceeds a certain threshold.

## Explanation by parts

## Retrieve the Processor Load Percentage:

```
$procesador = Get-WmiObject Win32_Processor
$proceso = $procesador.LoadPercentage
```
This code uses the Get-WmiObject cmdlet to access the Win32_Processor class from WMI, which provides information about the processor. The LoadPercentage property is then extracted and stored in the $loadPercentage variable.

## Check if the Load Percentage Exceeds 6:
```
if ($loadPercentage -gt 6)
```
This line checks if the processor's load percentage is greater than 6. If the condition is true, the code inside the if block is executed.

## Show a Warning Message Box:
```
[System.Windows.MessageBox]::Show('Processor load is high', 'Warning')
```
This line displays a message box with the title "Warning" and the message "Processor load is high". The `[System.Windows.MessageBox]::Show ` method is used for this.

## Create and Configure the Notification:
```
$balloon = New-Object System.Windows.Forms.NotifyIcon
```
This line creates a new NotifyIcon object which will be used to display a notification in the system tray.

## Set the Notification Icon:
```
try {
    $balloon.Icon = [System.Drawing.Icon]::ExtractAssociatedIcon((Get-Process -Name notepad).Path)
} catch {
    $balloon.Icon = [System.Drawing.SystemIcons]::Warning
}
```
This block tries to set the notification icon to the icon of the notepad process. If notepad is not running, it catches the error and sets a default warning icon instead. The try block ensures the script doesn't fail if notepad isn't found.

## Configure the Balloon Tip:
```
$balloon.BalloonTipIcon = [System.Windows.Forms.ToolTipIcon]::Info
$balloon.BalloonTipText = "Processor usage is at $loadPercentage%"
$balloon.BalloonTipTitle = "High Processor Load"
```
These lines set the properties for the balloon tip.

## Show the Notification:
```
$balloon.Visible = $true
$balloon.ShowBalloonTip(5000)
```
This makes the NotifyIcon visible in the system tray and displays the balloon tip for 5000 milliseconds (5 seconds).

## All the code
```
# Obtener el porcentaje de carga del procesador
$procesador = Get-WmiObject Win32_Processor
$proceso = $procesador.LoadPercentage

# Verificar si el porcentaje de carga es mayor que 6
if ($proceso -gt 6) {
    # Mostrar un cuadro de mensaje de advertencia
    [System.Windows.MessageBox]::Show('procesador','Warning')

    # Crear el objeto NotifyIcon para la notificación
    $balloon = New-Object System.Windows.Forms.NotifyIcon

    # Configurar la notificación
    # Icono (usar notepad si está en ejecución, de lo contrario, usar un icono predeterminado)
    try {
        $balloon.Icon = [System.Drawing.Icon]::ExtractAssociatedIcon((Get-Process -Name notepad).Path)
    } catch {
        $balloon.Icon = [System.Drawing.SystemIcons]::Warning
    }

    # Establecer el icono de la notificación
    $balloon.BalloonTipIcon = [System.Windows.Forms.ToolTipIcon]::Info

    # Establecer el mensaje de la notificación
    $balloon.BalloonTipText = "El uso del procesador es de $proceso%"

    # Establecer el título de la notificación
    $balloon.BalloonTipTitle = "Esto es malo"

    # Hacer visible el icono en la bandeja del sistema
    $balloon.Visible = $true

    # Mostrar la notificación durante 5 segundos
    $balloon.ShowBalloonTip(5000)
}
```
