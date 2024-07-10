# Verify Process Integrity Based on CPU Usage

## Explanation by parts

## Function Definition:
```
function comprobar ($integridadbuena)
```
Defines a function named comprobar that takes one parameter $integridadbuena.

## Retrieve the Process with the Highest CPU Usage and Compute its Hash:
```
$resultado = (Get-FileHash (ps | Sort-Object CPU | Select-Object -Last 1).Path).Hash
```
Retrieves the process with the highest CPU usage, computes the hash of its executable file, and stores the hash in $resultado.

## Compare Hash Values:
```
if(($integridadbuena) -eq $resultado){
    "es igual"
}
else{
    "no es igual"
}

```
Compares the known good hash with the computed hash and outputs "es igual" if they match or "no es igual" if they do not.

## Call the Function with a Known Good Hash:
```
comprobar (Get-Content archivo.txt)

```
Calls the comprobar function with the known good hash value read from archivo.txt.

## All the code
```
function comprobar ($integridadbuena)
{
    $resultado = (Get-FileHash (ps | sort cpu | select -Last 1).path).hash
    if(($integridadbuena) -eq $resultado){
    "es igual"
    }
    else{
    "no es igual"
    }
}

comprobar (Get-Content archivo.txt)

```