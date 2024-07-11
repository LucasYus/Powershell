# Retrieve Threads and Corresponding Services

## Explanation by parts

## Iterate Through Threads:
```
foreach ($i in Get-WmiObject -Class Win32_Thread | select Handle, ProcessHandle)

```
Iterates through each thread on the system, selecting only the Handle and ProcessHandle properties.

## Output Thread Handle:
```
$i.Handle

```
Outputs the handle of the current thread.

## Retrieve and Output Process Name:
```
"----" + (Get-Process -Id $i.ProcessHandle).Name

```
Retrieves and outputs the name of the process associated with the thread's ProcessHandle.

## Retrieve and Output Process ID:
```
"----" + (Get-Process -Id $i.ProcessHandle).Id

```
Retrieves and outputs the ID of the process associated with the thread's ProcessHandle.

## Retrieve and Output Parent Process Name:
```
"----------" + (Get-Process -Id ((Get-WmiObject -Class Win32_Process | where ProcessId -EQ (Get-Process -Id $i.ProcessHandle).Id).ParentProcessId)).Name

```
Retrieves and outputs the name of the parent process of the process associated with the thread's ProcessHandle.

# All the code
```
foreach ($i in Get-WmiObject -Class Win32_Thread | select Handle, ProcessHandle) {
    $i.Handle
    "----" + (Get-Process -Id $i.ProcessHandle).Name
    "----" + (Get-Process -Id $i.ProcessHandle).Id
    "----------" + (Get-Process -Id ((Get-WmiObject -Class Win32_Process | where ProcessId -EQ (Get-Process -Id $i.ProcessHandle).Id).ParentProcessId)).Name
}

```
