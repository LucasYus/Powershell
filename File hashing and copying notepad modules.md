# File Hashing and Copying Notepad Modules

## Explanation by parts

## Retrieve Notepad Process Modules:
```
(Get-Process -Name notepad).Modules.filename
```
Retrieves the filenames of all modules (DLLs) currently loaded by the Notepad process.

## Foreach Loop to Process Each Module:
```
foreach ($fichero in (Get-Process -Name notepad).Modules.filename) {
    ...
}
```
Iterates through each module file ($fichero) obtained from the previous step.

## Calculate File Hash:
```
Get-FileHash $fichero
```
Computes the hash value (SHA-256 by default) for the current module file ($fichero). The hash information is displayed in the console output.

## Copy Module File:
```
Copy-Item -Path $fichero -Destination .\copia.txt
```
Copies the current module file ($fichero) to the destination folder (.\copia.txt). If .\copia.txt is a folder, it copies the file into that folder with the same filename.

# All the code
```
foreach ($fichero in (Get-Process -Name notepad).Modules.filename) {
    Get-FileHash $fichero
    Copy-Item -Path $fichero -Destination .\copia.txt
}
```
