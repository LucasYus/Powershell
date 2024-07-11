# Basic Login Validation

## Explanation by parts

## Function Definition:
```
function login0 {
    param($user, $pass)

```
Defines a PowerShell function named login0 with two parameters: $user (username) and $pass (password).

## Begin Block:
```
begin {
    $useralmacenado = "juan"
    $passalmacenado = "1234"
}

```
Initializes the stored username ($useralmacenado) and password ($passalmacenado). This block runs once before the process block.

## Process Block:
```
process {
    if ($user -eq $useralmacenado -and $pass -eq $passalmacenado) {
        $resultado = 1
    } else {
        $resultado = 0
    }
}

```
Compares the input username ($user) and password ($pass) with the stored credentials.

## End Block:
```
end {
    if ($resultado -eq 1) {
        "inicia sesion"
    } else {
        $user, $pass | Out-File logs.txt -Append
    }
}

```
Executes after the process block.

# All the code
```
function login0 {
    param($user, $pass)
    
    begin {
        $useralmacenado = "juan"
        $passalmacenado = "1234"
    }
    
    process {
        if ($user -eq $useralmacenado -and $pass -eq $passalmacenado) {
            $resultado = 1
        } else {
            $resultado = 0
        }
    }
    
    end {
        if ($resultado -eq 1) {
            "inicia sesion"
        } else {
            $user, $pass | Out-File logs.txt -Append
        }
    }
}

```
