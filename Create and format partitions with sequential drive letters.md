# Create and Format Partitions with Sequential Drive Letters

## Explanation by parts

## Loop Through Character Codes:
```
foreach ($i in [int]'p'[0]..[int]'v'[0])

```
Iterates through the ASCII character codes of the letters 'P' to 'V'.

## Create New Partition:
```
New-Partition -DiskNumber 1 -Size 50MB -DriveLetter ([Char]$i)

```
Creates a new partition on DiskNumber 1 with a size of 50MB.

## Format Volume:
```
| Format-Volume
```
Formats the newly created partition with the default file system (usually NTFS).

# All the code
```
foreach ($i in [int]'p'[0]..[int]'v'[0]) {
    New-Partition -DiskNumber 1 -Size 50MB -DriveLetter ([Char]$i) | Format-Volume
}
```
