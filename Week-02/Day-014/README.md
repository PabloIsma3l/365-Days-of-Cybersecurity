# Day 14 – PowerShell Fundamentals (TryHackMe) 🟦⚡

## 🎯 Objective
Learn the fundamentals of Windows PowerShell, understand how cmdlets work, how objects are handled, and practice essential commands used for system administration and cybersecurity tasks.

---

## 🧠 What is PowerShell?
PowerShell is a **task automation and configuration management framework** built on .NET.  
It includes:
- A command-line shell
- A scripting language
- A powerful object-oriented pipeline

Unlike CMD, PowerShell works with **objects**, not plain text.

---

## 🔹 PowerShell Cmdlets

PowerShell commands are called **cmdlets** and follow a strict naming convention:


Examples:
- `Get-Process`
- `Get-Service`
- `Get-Command`
- `Get-Help`

This makes commands predictable and easy to discover.

---

## 📚 Discovering Commands

### `Get-Command`

sections:
  - name: Cmdlets Basics
    description: PowerShell uses cmdlets following the Verb-Noun format.
    content:
      - title: Verb-Noun Convention
        explanation: Lists available cmdlets and helps discover PowerShell capabilities.
        commands:
          - Get-Command
          - Get-Command -Verb Get
          - Get-Command -Noun Service
        notes:
          - Useful for discovering what PowerShell can do without memorizing commands.

      - title: Get-Help
        explanation: Displays built-in help information for cmdlets.
        commands:
          - Get-Help Get-Process
          - Get-Help Get-Process -Examples
          - Get-Help Get-Process -Full
        notes:
          - PowerShell includes powerful built-in documentation.

  - name: File System & Navigation
    content:
      - title: Get-ChildItem
        explanation: Lists files and directories (equivalent to ls or dir).
        commands:
          - Get-ChildItem
          - Get-ChildItem C:\Users
        aliases:
          - ls
          - dir

      - title: Set-Location
        explanation: Changes the current directory.
        commands:
          - Set-Location C:\Windows
          - cd C:\Windows

      - title: New-Item
        explanation: Creates new files or directories.
        commands:
          - New-Item file.txt
          - New-Item -ItemType Directory TestFolder

      - title: Remove-Item
        explanation: Deletes files or directories.
        commands:
          - Remove-Item file.txt
          - Remove-Item TestFolder -Recurse

      - title: Get-Content
        explanation: Reads file content.
        commands:
          - Get-Content file.txt

  - name: Processes & Services
    content:
      - title: Get-Process
        explanation: Lists running processes.
        commands:
          - Get-Process
          - Get-Process | Sort-Object CPU -Descending
        use_cases:
          - System monitoring
          - Detecting suspicious processes

      - title: Stop-Process
        explanation: Stops a running process.
        commands:
          - Stop-Process -Id 1234

      - title: Get-Service
        explanation: Lists services on the system.
        commands:
          - Get-Service
          - Get-Service | Where-Object {$_.Status -eq "Running"}

      - title: Start-Service / Stop-Service
        explanation: Starts or stops services.
        commands:
          - Start-Service wuauserv
          - Stop-Service wuauserv

  - name: PowerShell Pipeline
    description: PowerShell allows chaining commands using the pipeline.
    example:
      - Get-Service | Where-Object {$_.Status -eq "Stopped"}
    notes:
      - PowerShell passes objects, not text.

  - name: Filtering & Objects
    content:
      - title: Where-Object
        explanation: Filters output.
        commands:
          - Get-Process | Where-Object {$_.CPU -gt 100}

      - title: Select-Object
        explanation: Selects specific properties.
        commands:
          - Get-Process | Select-Object Name, Id, CPU

      - title: Sort-Object
        explanation: Sorts results.
        commands:
          - Get-Process | Sort-Object CPU

  - name: User & System Information
    content:
      - title: whoami
        explanation: Displays the current user.
        commands:
          - whoami

      - title: Get-ComputerInfo
        explanation: Displays system information.
        commands:
          - Get-ComputerInfo

      - title: Get-LocalUser
        explanation: Lists local users.
        commands:
          - Get-LocalUser

      - title: Get-LocalGroup
        explanation: Lists local groups.
        commands:
          - Get-LocalGroup

      - title: Get-LocalGroupMember
        explanation: Lists group members.
        commands:
          - Get-LocalGroupMember Administrators
        notes:
          - Important for privilege enumeration.

  - name: Execution Policy
    content:
      - title: Get-ExecutionPolicy
        explanation: Checks the current script execution policy.
        commands:
          - Get-ExecutionPolicy
        policies:
          - Restricted
          - AllSigned
          - RemoteSigned
          - Unrestricted
        warning:
          - Execution Policy is not a security boundary.

key_takeaways:
  - PowerShell uses cmdlets, not commands
  - Everything is an object
  - Pipelines enable powerful data manipulation
  - Built-in help makes learning easier
  - PowerShell is heavily used in real-world environments



