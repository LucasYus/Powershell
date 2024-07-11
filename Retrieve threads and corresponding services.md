# Retrieve Threads and Corresponding Services

## Explanation by parts

## Iterate Through Threads:
```
foreach ($hilo in Get-WmiObject -Class Win32_Thread)

```
Iterates through each thread on the system.

## Print Thread Handle and Process Handle:
```
Write-Host $hilo.Handle "->" $hilo.ProcessHandle

```
Outputs the handle of the current thread ($hilo.Handle) and the handle of the process to which the thread belongs ($hilo.ProcessHandle).

## Retrieve and Print Service Name:
```
Get-WmiObject Win32_Service | where ProcessId -EQ $hilo.ProcessHandle | select Name

```
Retrieves the name of the service associated with the process handle.

# All the code
```
foreach ($hilo in Get-WmiObject -Class Win32_Thread) {
    Write-Host $hilo.Handle "->" $hilo.ProcessHandle

    Get-WmiObject Win32_Service | where ProcessId -EQ $hilo.ProcessHandle | select Name
}

```
