# QR Code Generation, Display, and Decoding

## Explanation by parts

## Generate QR Code:
```
$var = "messages"
powershell.exe Write-Host $var | wsl qrencode -o fich.png
```
Sets the message to be encoded into a QR code ($var). Uses qrencode via WSL to generate a PNG file named fich.png containing the QR code.

## Display the QR Code:
```
.\fich.png
```
Displays the generated QR code file (fich.png) using the default application for PNG files.

## Encode the QR Code to Base 64:
```
$path = ".\fich.png"
$base64 = [System.Convert]::ToBase64String((Get-Content $path -Encoding Byte))
```
Reads the content of the QR code file (fich.png), converts it to a Base 64 string using [System.Convert]::ToBase64String, and stores the result in $base64.

## Open the Base 64 Encoded QR Code in Google Chrome:
```
Start-Process chrome "data:image/png;base64,$base64"
```
Opens Google Chrome and displays the Base 64 encoded QR code as an image directly in the browser.

## Save the Base 64 Encoded Image as a PNG File:
```
$bytes = [Convert]::FromBase64String($base64)
[IO.File]::WriteAllBytes("imagen.png", $bytes)
```
Decodes the Base 64 encoded string ($base64) back into bytes and writes those bytes to a file named imagen.png, saving it as a PNG image file.

## Decode the QR Code Using zbar:
```
wsl zbarimg imagen.png
```
Executes zbarimg via WSL to decode the QR code from the imagen.png file. This assumes that you have WSL installed and zbar properly configured for QR code decoding.

# All the code
```
# Message to be converted to a QR code using qrencode
$var = "messages"  # Message to convert to QR code
$var.Length  # Check the length of the message (optional)

# Create QR code with the information in $var
powershell.exe Write-Host $var | wsl qrencode -o fich.png

# Display the generated QR file
.\fich.png

# Encode the QR code to Base 64
$path = ".\fich.png"
$base64 = [System.Convert]::ToBase64String((Get-Content $path -Encoding Byte))

# Open the Base 64 encoded QR code in Google Chrome
Start-Process chrome "data:image/png;base64,$base64"

# Save the Base64-encoded image as a PNG file
$bytes = [Convert]::FromBase64String($base64)
[IO.File]::WriteAllBytes("imagen.png", $bytes)

# Run zbar to decode the QR code (requires WSL and zbar)
wsl zbarimg imagen.png

```
