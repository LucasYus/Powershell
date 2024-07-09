## Detect the evil hash of a file and report it with a message

## Explanation by parts

## Iterating through Notepad's Modules
```
foreach ($modulo in (Get-Process -Name notepad -Module | Select-Object -ExpandProperty FileName))
```
This line gets all the modules loaded by the notepad process.

## Calculating and Checking the File Hash
```
if ((Get-FileHash $modulo).Hash -eq "Put the hash here")
```
If the hash matches, the code inside the if block is executed.

## Show a Warning Message Box:
```
[System.Windows.MessageBox]::Show('Hash found', 'Warning')
```
This line displays a message box with the title "Warning" and the message "Hash found". The [System.Windows.MessageBox]::Show  method is used for this.

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
$balloon.BalloonTipText = "The module $modulo has the specified hash."
$balloon.BalloonTipTitle = "Esto es malo"
```
These lines set the properties for the balloon tip.

## Show the Notification:
```
$balloon.Visible = $true
$balloon.ShowBalloonTip(5000)

```
This makes the NotifyIcon visible in the system tray and displays the balloon tip for 5000 milliseconds (5 seconds).

## All the code
´´´
foreach ($modulo in (Get-Process -Name notepad -Module | Select-Object -ExpandProperty FileName)) {
    if ((Get-FileHash $modulo).Hash -eq "Put the hash here") {
        [System.Windows.MessageBox]::Show('Hash found', 'Warning')
        $balloon = New-Object System.Windows.Forms.NotifyIcon

        # Configure notification
        # Icon
        try {
            $balloon.Icon = [System.Drawing.Icon]::ExtractAssociatedIcon((Get-Process -Name notepad).Path)
        } catch {
            $balloon.Icon = [System.Drawing.SystemIcons]::Warning
        }
        # Set BalloonTipIcon
        $balloon.BalloonTipIcon = [System.Windows.Forms.ToolTipIcon]::Info

        # Message
        $balloon.BalloonTipText = "The module $modulo has the specified hash."

        # Title
        $balloon.BalloonTipTitle = "Esto es malo"

        $balloon.Visible = $true
        $balloon.ShowBalloonTip(5000)
    }
}
```
