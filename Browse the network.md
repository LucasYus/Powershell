# Browse the network

## Explanation by parts

## Define the IP Range and Iterate:
```
foreach ($ip in 1..254)
```
Iterates over the range of IP addresses from 1 to 254.

## Construct the Current IP Address:
```
$currentIP = "10.20.204." + $ip
```
Constructs the current IP address by appending the loop variable $ip to the base IP address "10.20.204.".

## Ping the Current IP Address:
```
$resultado = Test-Connection -ComputerName $currentIP -Count 1 -ErrorAction SilentlyContinue
```
Pings the current IP address once and stores the result in $resultado. Suppresses errors silently.

## Check if the Ping was Successful:
```
if ($resultado.StatusCode -eq 0)
```
Checks if the ping was successful by comparing the status code to 0.

## Iterate Over the Ping Replies:
```
foreach ($reply in $resultado)
```
Iterates over each reply in the ping result.

## Check if the Reply Address Matches the Current IP:
```
if ($reply.Address -eq $currentIP)
```
Checks if the reply's address matches the current IP address.

## Extract and Output TTL:
```
$ttl = $reply.ResponseTime
Write-Output "IP: $currentIP, TTL: $ttl"
```
Extracts the TTL (time to live) value from the reply and outputs the current IP address and TTL.

## Retrieve and Output MAC Address:
```
$macAddress = (Get-NetNeighbor | Where-Object { $_.IpAddress -eq $currentIP }).LinkLayerAddress
Write-Output "IP: $currentIP, MAC Address: $macAddress"
```
Retrieves the MAC address associated with the current IP address using Get-NetNeighbor and outputs the current IP address and MAC address.

# All the code
```
foreach ($ip in 1..254)
{
    $currentIP = "10.20.204." + $ip
    $resultado = Test-Connection -ComputerName $currentIP -Count 1 -ErrorAction SilentlyContinue

    if ($resultado.StatusCode -eq 0)
    {
        foreach ($reply in $resultado)
        {
            if ($reply.Address -eq $currentIP)
            {
                $ttl = $reply.ResponseTime
                Write-Output "IP: $currentIP, TTL: $ttl"
            }
        }

        $macAddress = (Get-NetNeighbor | Where-Object { $_.IpAddress -eq $currentIP }).LinkLayerAddress
        Write-Output "IP: $currentIP, MAC Address: $macAddress"
    }
}

```
