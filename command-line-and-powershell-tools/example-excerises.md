# 🏃‍♂️ Example Excerises

## PowerShell Practice Notes

***

### 🔹 Basic Notes

* **ISE (Integrated Scripting Environment):** A GUI for writing and debugging PowerShell scripts.
* **Everything in PowerShell is an OBJECT** ✅
*   **Check PowerShell version:**

    ```powershell
    $PSVersionTable.PSVersion
    ```
*   **Ping a website:**

    ```powershell
    ping spacex.com
    ```

***

### 🎓 Learning Tools

* **Videos Used:** [PowerShell Tutorial](https://youtu.be/ZOoCaWyifmI?si=rMnplrySHUomcHLh)

***

### 🔹 About Cmdlets

* **Cmdlet format:** `Verb-Noun` (unless it's a custom function).
*   **Check execution policy:**

    ```powershell
    Get-ExecutionPolicy
    ```
*   **Change execution policy:**

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```
* `RemoteSigned` allows custom scripts to run.

***

### 📝 Basic Cmdlets

*   **Print text:**

    ```powershell
    Write-Host "Hello World! " -NoNewline
    Write-Host "Hello Again!"
    ```
*   **Find commands:**

    ```powershell
    Get-Command
    Get-Command -CommandType Cmdlet
    ```
*   **Get help for a command:**

    ```powershell
    Get-Help Write-Host -Full
    ```

***

### 🔗 Piping Cmdlets

*   **Write to a file:**

    ```powershell
    "May the force be with you!" | Out-File forcewithwho.txt
    ```
*   **View file content:**

    ```powershell
    Get-Content .\forcewithwho.txt
    ```

***

### 🔹 Variables

*   **Create a variable:**

    ```powershell
    $FavCharacter = "Spongebob"
    ```
*   **Output a variable:**

    ```powershell
    Write-Output $FavCharacter
    ```
*   **Save variable to a file:**

    ```powershell
    $FavCharacter | Out-File FavCharacter.txt
    Get-Content .\FavCharacter.txt
    ```
*   **Find variable type:**

    ```powershell
    $FavCharacter.GetType()
    ```
*   **List all properties:**

    ```powershell
    $FavCharacter | Select-Object -Property *
    ```
*   **List all methods:**

    ```powershell
    Get-Member -InputObject $FavCharacter
    ```

***

### 🔹 Arrays

*   **Define an array:**

    ```powershell
    $Jedi = @("Matthew","Mark","Luke","John")
    ```
*   **Get first element:**

    ```powershell
    $Jedi[0]  # Arrays start at index 0
    ```
*   **Add an element:**

    ```powershell
    $Jedi += "David"
    ```

***

### 🔹 HashTables

*   **Define a hashtable:**

    ```powershell
    $Family = @{David = "Dad"; Steph ="Mum"; Charlotte ="Daughter"}
    ```
*   **Add an entry:**

    ```powershell
    $Family.Add("Midnight","Cat")
    ```

***

### 🏗️ Collecting User Input

*   **Prompt for user input:**

    ```powershell
    Write-Host "What is your favorite game system?"
    Write-Host "1. NES"
    Write-Host "2. Wii"
    Write-Host "3. N64"
    $FavSystem = Read-Host "Fav game system?"
    ```

***

### 🔹 Conditional Statements

*   **If-Else Example:**

    ```powershell
    $PokemonCaught = 808
    If ($PokemonCaught -eq 908) {
        Write-Host "You're a Pokemon Master!"
    } Else {
        Write-Host "Go catch more Pokemon!"
    }
    ```
*   **ElseIf Example:**

    ```powershell
    $PokemonNum = 200
    If($PokemonNum -ge 0 -and $PokemonNum -le 151) {
        Write-Host "Your Pokemon is from Kanto!"
    } ElseIf ($PokemonNum -ge 152 -and $PokemonNum -le 251) {
        Write-Host "Your Pokemon is from Johto!"
    }
    ```

***

### 🔹 Loops

*   **For Loop:**

    ```powershell
    $Pets = @("cat","dog","fish","lizard","snake")
    For ($counter = 0; $counter -lt $Pets.Length; $counter++) {
        Write-Host "Hey, it's" $Pets[$counter]
    }
    ```
*   **ForEach Loop:**

    ```powershell
    Foreach ($Pet in $Pets) {
        Write-Host $Pet "has arrived!"
    }
    ```
*   **While Loop:**

    ```powershell
    $Office = @("Jim","Pam","Dwight","Michael")
    $counter = 0
    While ($counter -lt $Office.Length) {
        Write-Host $Office[$counter] "is going to the Mall! "
        $counter++
    }
    ```

***

### 🔹 Functions

*   **Define a function:**

    ```powershell
    function Test-SpaceX {
        [CmdletBinding()]
        param(
            [Parameter(Mandatory)]
            [int32]$PingCount
        )
        Test-Connection spacex.com -Count $PingCount
    }
    Test-SpaceX -PingCount 3
    ```

***

### 🔹 Error Handling

*   **Using Try-Catch:**

    ```powershell
    try {
        Test-SpaceX -PingCount 3
    } catch {
        Write-Output "Launch Problem"
        Write-Output $_
    }
    ```

***

### 🔹 File Operations

*   **Create a file:**

    ```powershell
    New-Item -Path "C:\Users\YourName\Documents\ewok.txt" -ItemType "file" -Value "Praise C3PO!"
    ```
*   **Move a file:**

    ```powershell
    Move-Item -Path "C:\Users\YourName\Documents\ewok.txt" -Destination "C:\Users\YourName\Documents\Scripts\"
    ```
*   **Delete a file:**

    ```powershell
    Remove-Item .\ewok.txt
    ```

***

### 🔹 Active Directory (Admin Mode)

*   **Import Active Directory Module:**

    ```powershell
    Import-Module ActiveDirectory
    ```
*   **Get a user:**

    ```powershell
    Get-ADUser fbaggins
    ```
*   **Create a new AD user:**

    ```powershell
    New-ADUser -Name "Luke Skywalker" -GivenName "Luke" -Surname "Skywalker" -SamAccountName "lskywalker" -UserPrincipalName "lskywalker@email.com"
    ```

***

### ⚡ Quick Tip

* Use `Clear-Host` to clear the console screen.
* Use `Get-Process | Sort-Object WorkingSet64 -Descending | Select-Object -First 10` to find top 10 memory-consuming processes.

***
