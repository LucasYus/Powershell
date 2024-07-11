# Combine Lines from Two Files and Execute as Command

## Explanation by parts

## For Loop Initialization:
```
for ($i = 0; $i -lt (Get-Content .\archivo1.txt).Length; $i++) {

```
Initializes a for loop to iterate through the lines of archivo1.txt.

## Combine Corresponding Lines:
```
(Get-Content .\archivo1.txt)[$i] + " " + (Get-Content .\archivo2.txt)[$i]

```
Reads the $i-th line from both archivo1.txt and archivo2.txt, combines them into a single string separated by a space.

## Execute Combined Line:
```
| iex

```
Pipes the combined string to iex (Invoke-Expression) to execute it as a PowerShell command.

# All the code
```
for ($i = 0; $i -lt (Get-Content .\archivo1.txt).Length; $i++) {
    (Get-Content .\archivo1.txt)[$i] + " " + (Get-Content .\archivo2.txt)[$i] | iex
}

```
