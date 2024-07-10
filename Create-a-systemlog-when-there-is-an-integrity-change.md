# Create a systemlog when there is an integrity change

## Explanation by parts

## Function Definition:
```
function comprobar ($integridadbuena)
```
Defines a function named comprobar that takes one parameter $integridadbuena.

## Retrieve the Process with the Highest CPU Usage:
```
$cpuproceso = Get-Process | Sort-Object CPU | Select-Object -Last 1
```
Retrieves the process with the highest CPU usage.

## Check if a Process is Found:
```
$cpuproceso = Get-Process | Sort-Object CPU | Select-Object -Last 1
```
Checks if a process was successfully retrieved and stored in $cpuproceso. If no process was found, this block is skipped.

## Compute the Hash of the Process:
```
$cpuproceso = Get-Process | Sort-Object CPU | Select-Object -Last 1
```
Computes the hash of the executable file of the process with the highest CPU usage.

## Compare Hash Values:
```
$cpuproceso = Get-Process | Sort-Object CPU | Select-Object -Last 1
```
Compares the known good hash ($integridadbuena) with the computed hash of the process ($resultado). 
If the hashes match, it outputs "es igual".
If the hashes do not match, it writes an event to the Windows event log.

## Call the Function with a Known Good Hash:
```
comprobar (Get-Content .\archivo.txt)
```
Reads the content of the file archivo.txt (which should contain the known good hash value) and passes it as an argument to the comprobar function.

## All the code
```
function comprobar ($integridadbuena) {
    
    $cpuproceso = Get-Process | Sort-Object CPU | Select-Object -Last 1
    if ($cpuproceso) {
        $resultado = (Get-FileHash $cpuproceso.Path).Hash

        
        if ($integridadbuena -eq $resultado) {
            "es igual"
        } else {
            
            Write-EventLog -LogName "Application" -Source "Microsoft-Windows-User-Loader" -EventId 916 -EntryType Information -Message "Mensaje ejemplo" -Category 2 -RawData 10,20
        }
    } else {
        Write-Output "No processes found."
    }
}

comprobar (Get-Content .\archivo.txt)
```