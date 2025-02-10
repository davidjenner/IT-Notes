# ⚡ Automation

Here’s an updated Automation & Scheduled Tasks section with both CMD and PowerShell commands laid out in a copy-friendly format.

🛠 Windows Automation & Scheduled Tasks (CMD + PowerShell)



Below are useful automation tasks using both Command Prompt (CMD) and PowerShell, allowing you to schedule tasks, automate maintenance, and manage system operations efficiently.

1️⃣ Schedule a Task to Run Every Night

\


✅ CMD:

```
schtasks /create /tn "NightlyTask" /tr "C:\Scripts\cleanup.bat" /sc daily /st 23:00
```

✅ PowerShell:

```
$Trigger = New-ScheduledTaskTrigger -Daily -At 11PM
$Action = New-ScheduledTaskAction -Execute "C:\Scripts\cleanup.bat"
Register-ScheduledTask -TaskName "NightlyCleanup" -Trigger $Trigger -Action $Action
```

📌 Purpose: Runs a cleanup script every night at 11 PM.

📌 Use Case: Automating log cleanups, backups, or maintenance.

2️⃣ Automatically Shutdown the PC at a Specific Time

\


✅ CMD:

```
shutdown /s /t 3600
```

✅ PowerShell:

```
Start-Sleep -Seconds 3600; Stop-Computer -Force
```

📌 Purpose: Shuts down the PC after 1 hour (3600 seconds).

📌 Use Case: Prevents computers from staying on overnight.

3️⃣ Restart the PC After a Set Time

\


✅ CMD:

```
shutdown /r /t 1800
```

✅ PowerShell:

```
Start-Sleep -Seconds 1800; Restart-Computer -Force
```

📌 Purpose: Restarts the PC after 30 minutes (1800 seconds).

📌 Use Case: Used after installing software updates.

4️⃣ Schedule a System Reboot Every Sunday at 2 AM

\


✅ CMD:

```
schtasks /create /tn "WeeklyReboot" /tr "shutdown /r /f /t 0" /sc weekly /d SUN /st 02:00
```

✅ PowerShell:

```
$Trigger = New-ScheduledTaskTrigger -Weekly -DaysOfWeek Sunday -At 2AM
$Action = New-ScheduledTaskAction -Execute "shutdown.exe" -Argument "/r /f /t 0"
Register-ScheduledTask -TaskName "WeeklyReboot" -Trigger $Trigger -Action $Action
```

📌 Purpose: Forces a system reboot every Sunday at 2 AM.

📌 Use Case: Ensures servers or workstations stay refreshed.

5️⃣ Empty the Recycle Bin Automatically

\


✅ PowerShell:

```
Clear-RecycleBin -Force
```

📌 Purpose: Deletes all items in the Recycle Bin.

📌 Use Case: Helps free up disk space automatically.

6️⃣ Uninstall a Program Silently

\


✅ CMD:

```
wmic product where "name='Program Name'" call uninstall /nointeractive
```

✅ PowerShell:

```
(Get-WmiObject -Class Win32_Product | Where-Object { $_.Name -eq "Program Name" }).Uninstall()
```

📌 Purpose: Removes a program silently without user prompts.

📌 Use Case: Useful for mass uninstallations.

7️⃣ Create a Backup of a Folder Daily

\


✅ CMD:

```
xcopy C:\ImportantFiles D:\Backup /E /I /Y
```

✅ PowerShell:

```
Copy-Item -Path "C:\ImportantFiles\*" -Destination "D:\Backup" -Recurse -Force
```

📌 Purpose: Backs up an entire folder to another drive.

📌 Use Case: Automates file backups.

8️⃣ Disable Windows Defender Temporarily

\


✅ PowerShell:

```
Set-MpPreference -DisableRealtimeMonitoring $true
```

📌 Purpose: Temporarily disables Windows Defender real-time protection.

📌 Use Case: Useful when installing trusted third-party software.

9️⃣ Enable Windows Defender Again

\


✅ PowerShell:

```
Set-MpPreference -DisableRealtimeMonitoring $false
```

📌 Purpose: Re-enables Windows Defender after temporary disabling.

🔟 One-Click Full System Cleanup

\


✅ PowerShell:

```
Write-Host "Starting System Cleanup..."
Start-Process "cleanmgr.exe" -ArgumentList "/sagerun:1" -NoNewWindow -Wait
Clear-RecycleBin -Force
Get-ChildItem "C:\Windows\Temp" -Recurse | Remove-Item -Force -Recurse
Write-Host "Cleanup Complete!"
```

📌 Purpose: Runs a disk cleanup, empties the Recycle Bin, and deletes temp files.

📌 Use Case: Automates cleanup tasks for better performance.

📌 How to Use These Scripts

1\. For CMD: Open Command Prompt (cmd.exe) as Administrator and paste the command.

2\. For PowerShell: Open PowerShell as Administrator and paste the script.

3\. For Automation: Add PowerShell scripts to Task Scheduler to run them automatically.

🔥 These automation scripts save time, optimize performance, and improve system efficiency! Let me know if you need more! 🚀
