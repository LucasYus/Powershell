# Check the size of a shared folder

## Explanation by parts

## Function Definition:
```
function quehaceunproceso ()

```
Defines a PowerShell function named quehaceunproceso.

## Read User Input:
```
$proceso = Read-Host "What process do you want to know information about?"
```
Prompts the user to input a process number or name. The input is stored in the variable $proceso.

## Process Selection Using if and elseif:
```
if ($proceso -eq 1)
{
    Get-Process | Select-Object Name, Threads
}
elseif ($proceso -eq 2)
{
    chrome
}

```
Depending on the value of $proceso, executes different actions.

## Invocation of the Function:
```
quehaceunproceso
```
Executes the quehaceunproceso function when the script is run, initiating the process information retrieval based on user input.

# All the code
```
function quehaceunproceso ()
{
    $proceso = Read-Host "What process do you want to know information about?"
    if ($proceso -eq 1)
    {
        Get-Process | Select-Object Name, Threads
    }
    elseif ($proceso -eq 2)
    {
        chrome
    }
}

quehaceunproceso
```