# 🚀 Troubleshoot with CMD & Powershell

Sure! Below is a comprehensive list of troubleshooting tools for both Command Prompt (CMD) and PowerShell, categorized by system diagnostics, network troubleshooting, performance monitoring, security, and repair tasks. Each tool includes example commands and explanations of when to use them.

🚀 Windows Troubleshooting Toolkit (CMD + PowerShell)

\


🔹 System Information & Diagnostics

| Task                          | CMD Command                               | PowerShell Command                                       | Purpose                                                   |
| ----------------------------- | ----------------------------------------- | -------------------------------------------------------- | --------------------------------------------------------- |
| Get System Information        | systeminfo                                | Get-ComputerInfo                                         | Retrieves details like OS version, RAM, uptime, and more. |
| Check System Uptime           | wmic os get LastBootUpTime                | (Get-CimInstance Win32\_OperatingSystem).LastBootUpTime  | Shows the last time the PC was restarted.                 |
| View Recent System Errors     | wevtutil qe System /c:10 /rd:true /f:text | Get-EventLog -LogName System -Newest 10 -EntryType Error | Retrieves the latest system errors from the Event Viewer. |
| Generate a Performance Report | perfmon /report                           | perfmon /report                                          | Runs a 60-second diagnostic test on system performance.   |

📡 Network Troubleshooting

| Task                            | CMD Command         | PowerShell Command                                                     | Purpose                                                                    |
| ------------------------------- | ------------------- | ---------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Check IP Configuration          | ipconfig /all       | Get-NetIPConfiguration                                                 | Displays network adapter settings, IP, DNS, and MAC addresses.             |
| Flush DNS Cache                 | ipconfig /flushdns  | Clear-DnsClientCache                                                   | Fixes DNS issues, such as slow or failed webpage loading.                  |
| Test Internet Connection        | ping google.com     | Test-NetConnection -ComputerName google.com -InformationLevel Detailed | Tests if the PC can reach the internet.                                    |
| List Active Network Connections | netstat -ano        | Get-NetTCPConnection                                                   | Identifies open ports, remote connections, and potential malware activity. |
| Reset Network Settings          | netsh winsock reset | netsh winsock reset                                                    | Fixes network issues by resetting Winsock.                                 |

🖥 Performance & Process Monitoring

| Task                        | CMD Command                                                                    | PowerShell Command                     | Purpose                                        |
| --------------------------- | ------------------------------------------------------------------------------ | -------------------------------------- | ---------------------------------------------- |
| View Running Processes      | tasklist                                                                       | Get-Process                            | Lists all active processes.                    |
| Kill a Process              | taskkill /IM notepad.exe /F                                                    | Stop-Process -Name notepad -Force      | Forcefully stops an unresponsive program.      |
| Check CPU Usage             | wmic cpu get loadpercentage                                                    | \`Get-WmiObject win32\_processor       | Select-Object -ExpandProperty LoadPercentage\` |
| Check Memory Usage          | wmic OS get FreePhysicalMemory                                                 | Get-Counter "\Memory\Available MBytes" | Shows available RAM on the system.             |
| Monitor Real-Time CPU Usage | wmic path Win32\_PerfFormattedData\_PerfOS\_Processor get PercentProcessorTime | \`Get-Process                          | Sort-Object CPU -Descending                    |

💾 Disk & Storage Analysis

| Task                               | CMD Command                                 | PowerShell Command                     | Purpose                                                |
| ---------------------------------- | ------------------------------------------- | -------------------------------------- | ------------------------------------------------------ |
| Check Disk Usage                   | wmic logicaldisk get caption,freespace,size | \`Get-Volume                           | Select-Object DriveLetter, FileSystem, SizeRemaining\` |
| List & Check Drive Health          | wmic diskdrive get model,status             | \`Get-PhysicalDisk                     | Select-Object FriendlyName, HealthStatus\`             |
| Run CHKDSK (Check Disk for Errors) | chkdsk /f                                   | Repair-Volume -DriveLetter C           | Scans and fixes drive errors.                          |
| Defragment a Drive                 | defrag C:                                   | Optimize-Volume -DriveLetter C -Defrag | Optimizes file storage for better performance.         |

🔧 System Repair & Maintenance

| Task                                      | CMD Command                                        | PowerShell Command                                         | Purpose                                         |
| ----------------------------------------- | -------------------------------------------------- | ---------------------------------------------------------- | ----------------------------------------------- |
| Check & Repair Corrupt System Files       | sfc /scannow                                       | sfc /scannow                                               | Scans and repairs corrupt Windows system files. |
| Fix Advanced System Corruption            | DISM /Online /Cleanup-Image /RestoreHealth         | DISM /Online /Cleanup-Image /RestoreHealth                 | Fixes deeper Windows image issues.              |
| Restart Windows Explorer (Fix UI Freezes) | taskkill /IM explorer.exe /F && start explorer.exe | Stop-Process -Name explorer -Force; Start-Process explorer | Fixes an unresponsive taskbar or Start menu.    |
| Restart Windows Update Service            | net stop wuauserv && net start wuauserv            | Restart-Service wuauserv                                   | Fixes Windows Update errors.                    |

🔒 Security & User Management

| Task                                | CMD Command                                 | PowerShell Command                                         | Purpose                              |
| ----------------------------------- | ------------------------------------------- | ---------------------------------------------------------- | ------------------------------------ |
| List All User Accounts              | net user                                    | Get-LocalUser                                              | Displays all local user accounts.    |
| Check if a User is an Administrator | net localgroup Administrators               | Get-LocalGroupMember Administrators                        | Lists admin users on the system.     |
| Enable a Disabled Account           | net user username /active:yes               | Enable-LocalUser -Name "username"                          | Re-enables a disabled user account.  |
| Check for Failed Login Attempts     | wevtutil qe Security /c:10 /rd:true /f:text | Get-EventLog -LogName Security -InstanceId 4625 -Newest 10 | Detects unauthorized login attempts. |

🛠 Automation & Scheduled Tasks

| Task                               | CMD Command                                                                         | PowerShell Command                              | Purpose                                                                                                                 |
| ---------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Schedule a Task to Run Every Night | schtasks /create /tn "NightlyTask" /tr "C:\Scripts\cleanup.bat" /sc daily /st 23:00 | \`New-ScheduledTaskTrigger -Daily -At 11PM      | Register-ScheduledTask -Action (New-ScheduledTaskAction -Execute ‘C:\Scripts\cleanup.bat’) -TaskName “NightlyCleanup”\` |
| Shutdown PC at a Specific Time     | shutdown /s /t 3600                                                                 | Start-Sleep -Seconds 3600; Stop-Computer -Force | Automatically shuts down the PC.                                                                                        |
| Uninstall a Program Silently       | wmic product where "name='Program Name'" call uninstall /nointeractive              | \`(Get-WmiObject -Class Win32\_Product          | Where-Object { $\_.Name -eq “Program Name” }).Uninstall()\`                                                             |

🔥 BONUS: One-Click Full System Health Check (PowerShell)

\


This script collects key diagnostic data into a single log file:

```
$ReportPath = "C:\PC_Health_Report.txt"
Get-ComputerInfo | Out-File $ReportPath
Get-NetIPConfiguration | Out-File -Append $ReportPath
Get-PhysicalDisk | Out-File -Append $ReportPath
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 | Out-File -Append $ReportPath
Get-EventLog -LogName System -Newest 10 | Out-File -Append $ReportPath
Write-Host "System Health Report saved to $ReportPath"
```

✅ How to Use: Run this before troubleshooting to gather system info in one place.

💡 These CMD & PowerShell tools help IT professionals diagnose and resolve Windows issues efficiently! Let me know if you need automation scripts! 🚀
