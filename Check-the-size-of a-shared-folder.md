# Check the size of a shared folder

## Explanation by parts

## Shared Folder Path:
```
$sharedFolderPath = "\\ServerName\SharedFolder"
```
The variable $sharedFolderPath defines the path to the shared folder (\\ServerName\SharedFolder). Replace "\\ServerName\SharedFolder" with the actual path of your shared folder.

## Define Total Size Threshold:
```
$total = 100 * 1GB
```
Sets $total to 100 GB converted to bytes. In PowerShell, 1GB is a predefined constant representing 1 gigabyte (1,073,741,824 bytes).

## Retrieve Total Size of Files in Shared Folder:
```
$totalSize = (Get-ChildItem -Path $sharedFolderPath -File -Recurse | Measure-Object -Property Length -Sum).Sum

```
The command Get-ChildItem -Path $sharedFolderPath -File -Recurse is used to explore and gather information about all files within the specified shared folder ($sharedFolderPath).
## Comparison:
```
if ($totalSize -lt $total * 0.8) {
    "less"
}
```
Checks if the $totalSize (total size of files in the shared folder) is less than 80% of $total.

## All the code
```
$sharedFolderPath = "\\ServerName\SharedFolder"  # Reemplaza con la ruta de tu carpeta compartida

$total = 100 * 1GB  # 100 GB en bytes, asumiendo que $total es 100 GB


$totalSize = (Get-ChildItem -Path $sharedFolderPath -File -Recurse | Measure-Object -Property Length -Sum).Sum


if ($totalSize -lt $total * 0.8) {
    "menor"
}
```
