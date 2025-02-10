# 🔍 Analysis

Here are more advanced diagnostic and analysis commands that IT technicians can use to get an overview of system performance, detect bottlenecks, and troubleshoot technical issues on a Windows PC.

System Performance & Resource Monitoring

1\. Check CPU Usage (Live Updates)

```
wmic cpu get loadpercentage
```

• Purpose: Shows current CPU usage in percentage.

• When to Use: When diagnosing high CPU usage or system slowdowns.

\


2\. Monitor CPU Usage Over Time

```
typeperf "\Processor(_Total)\% Processor Time" -si 5
```

• Purpose: Displays CPU usage updates every 5 seconds.

• When to Use: When analyzing CPU load trends.

\


3\. Check Memory Usage

```
wmic OS get FreePhysicalMemory,TotalVisibleMemorySize
```

• Purpose: Displays available and total RAM in kilobytes.

• When to Use: When investigating memory leaks or insufficient RAM.

\


4\. Check Processes Sorted by Memory Usage

```
wmic process get name,workingsetsize | sort /r
```

• Purpose: Lists processes consuming the most RAM.

• When to Use: When troubleshooting memory-hungry applications.

\


5\. Check Disk Usage by System Processes

```
wmic path Win32_PerfFormattedData_PerfDisk_LogicalDisk get Name,PercentDiskTime
```

• Purpose: Identifies high disk usage.

• When to Use: When investigating slow disk performance.

\


6\. Check Power Consumption & Battery Health _(Laptops Only)_

```
powercfg /batteryreport
```

• Purpose: Generates a detailed battery report.

• When to Use: When troubleshooting power-related issues.

\


7\. Check System Uptime

```
net statistics workstation | find "Statistics since"
```

• Purpose: Shows how long the system has been running.

• When to Use: To determine if a reboot is necessary.

Network Troubleshooting & Analysis

8\. Check Active Network Connections & Their Processes

```
netstat -abno
```

• Purpose: Lists open network connections and the processes using them.

• When to Use: When investigating potential malware or unauthorized connections.

\


9\. List All Active Network Adapters

```
netsh interface show interface
```

• Purpose: Displays all network interfaces and their statuses.

• When to Use: When checking for disabled or disconnected adapters.

\


10\. Test Network Packet Loss (Continuous Ping)

```
ping 8.8.8.8 -t
```

• Purpose: Sends continuous pings to detect packet loss.

• When to Use: When troubleshooting unstable internet connections.

\


11\. Find Latency Issues in Network Route

```
pathping google.com
```

• Purpose: Provides detailed latency and packet loss statistics along a network path.

• When to Use: When diagnosing slow network speeds.

\


12\. Check Network Adapter Driver Issues

```
pnputil /enum-devices /class net
```

• Purpose: Lists network adapters and their driver details.

• When to Use: When identifying faulty or outdated network drivers.

Event Logs & System Errors

13\. Check Recent Critical System Errors

```
wevtutil qe System /c:20 /f:text /rd:true /q:"*[System[(Level=1 or Level=2)]]"
```

• Purpose: Retrieves the last 20 critical or error-level events from the system log.

• When to Use: When diagnosing crashes, unexpected shutdowns, or system failures.

\


14\. View Recent Application Errors

```
wevtutil qe Application /c:10 /f:text /rd:true
```

• Purpose: Lists the last 10 application errors.

• When to Use: When diagnosing software crashes.

\


15\. Check Windows Update Failure Logs

```
Get-WindowsUpdateLog
```

• Purpose: Retrieves logs for failed Windows Updates.

• When to Use: When updates are failing to install.

\


16\. Check System Boot Time Logs

```
systeminfo | find "Boot Time"
```

• Purpose: Shows when the system last booted up.

• When to Use: When checking for unexpected reboots.

Storage & Disk Performance

17\. Check Disk I/O Performance (Read/Write Speed)

```
winsat disk -seq -read -write
```

• Purpose: Measures disk performance.

• When to Use: When diagnosing slow disk speeds.

\


18\. List Disk Partitions & Sizes

```
wmic partition get Name,Size
```

• Purpose: Displays partition information.

• When to Use: When checking for unallocated space or disk structure issues.

\


19\. Check SSD/HDD Health Using SMART Data

```
wmic diskdrive get status
```

• Purpose: Retrieves disk health status (OK, BAD, WARNING).

• When to Use: When suspecting failing hard drives.

Software & System Configuration Checks

20\. List Installed Software with Install Dates

```
wmic product get name,version,installdate
```

• Purpose: Displays installed programs and their install dates.

• When to Use: When looking for recently installed problematic software.

\


21\. Check Running Services (Status & Auto-Start Services)

```
wmic service get name,startmode,state
```

• Purpose: Lists all services and their startup mode.

• When to Use: When diagnosing startup delays or service failures.

\


22\. Identify Auto-Starting Programs

```
wmic startup get caption,command
```

• Purpose: Displays programs that launch at startup.

• When to Use: When troubleshooting slow boot times.

\


23\. Check Current Group Policy Settings

```
gpresult /h C:\gp_report.html
```

• Purpose: Generates a report of applied Group Policy settings.

• When to Use: When verifying security policies or troubleshooting domain policy issues.

Malware & Unauthorized Access Detection

24\. Check for Hidden User Accounts

```
net user
```

• Purpose: Lists all user accounts on the system.

• When to Use: When checking for unauthorized accounts.

\


25\. List All Scheduled Tasks

```
schtasks /query /fo LIST /v
```

• Purpose: Shows all scheduled tasks, including potential malware persistence mechanisms.

• When to Use: When looking for hidden malicious tasks.

\


26\. Check for Unauthorized Remote Access

```
qwinsta
```

• Purpose: Displays active remote desktop sessions.

• When to Use: When investigating potential remote access breaches.

\


27\. List Active User Sessions

```
query user
```

• Purpose: Shows currently logged-in users.

• When to Use: When checking for unauthorized logins.

These additional troubleshooting commands provide deep insight into system performance, errors, and potential technical issues. IT technicians can use them to quickly diagnose and resolve problems on a Windows PC. 🚀

\


Would you like a batch script or PowerShell automation to make running these easier? 😊
