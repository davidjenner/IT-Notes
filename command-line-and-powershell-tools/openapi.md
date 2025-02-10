---
icon: network-wired
---

# Troubleshoot with CMD

Here is an improved version of the command-line snippets for IT technicians, including descriptions of when to use them and their purposes.

System Information & Diagnostics

1\. Check System Information

```
systeminfo
```

• Purpose: Displays OS details, installed updates, uptime, and system specifications.

• When to Use: When diagnosing system issues or gathering system details for troubleshooting.

\


2\. Check Computer Name & Workgroup

```
hostname
```

```
echo %COMPUTERNAME%
```

• Purpose: Retrieves the current computer name.

• When to Use: When identifying the system in a networked environment.

\


3\. Check IP Configuration & Network Status

```
ipconfig /all
```

• Purpose: Displays detailed network adapter configuration, including IP addresses, gateways, and DNS settings.

• When to Use: When troubleshooting network connectivity issues.

\


4\. Test Network Connectivity (Ping/Tracert/NSLookup)

```
ping google.com
```

• Purpose: Checks if a host is reachable and measures response time.

• When to Use: When troubleshooting internet or internal network connectivity.

```
tracert google.com
```

• Purpose: Traces the route packets take to reach a destination.

• When to Use: When diagnosing slow connections or routing issues.

```
nslookup google.com
```

• Purpose: Queries DNS to resolve domain names to IP addresses.

• When to Use: When investigating DNS resolution issues.

\


5\. Check Open Network Connections

```
netstat -ano
```

• Purpose: Displays active connections and listening ports, including associated process IDs.

• When to Use: When diagnosing potential malware, unauthorized connections, or network bottlenecks.

\


6\. Check Firewall Rules

```
netsh advfirewall show allprofiles
```

• Purpose: Displays Windows Firewall status and rules.

• When to Use: When checking if the firewall is blocking a service or connection.

\


7\. Check DNS Cache

```
ipconfig /displaydns
```

• Purpose: Shows cached DNS records.

• When to Use: When verifying if DNS resolution issues are due to outdated cache entries.

\


8\. Flush DNS Cache (Fix DNS Issues)

```
ipconfig /flushdns
```

• Purpose: Clears the DNS resolver cache.

• When to Use: When resolving DNS-related connectivity problems.

\


9\. Release & Renew IP Address

```
ipconfig /release && ipconfig /renew
```

• Purpose: Releases the current IP address and requests a new one.

• When to Use: When troubleshooting DHCP and IP conflicts.

Process & Service Management

10\. List Running Processes

```
tasklist
```

• Purpose: Displays all running processes.

• When to Use: When identifying rogue or resource-heavy processes.

\


11\. Kill a Process by Name or ID

```
taskkill /IM notepad.exe /F
```

```
taskkill /PID 1234 /F
```

• Purpose: Terminates a running process forcefully.

• When to Use: When a program is unresponsive or consuming excessive resources.

\


12\. List Running Services

```
net start
```

• Purpose: Displays all running services.

• When to Use: When checking if necessary services are active.

\


13\. Restart a Service

```
net stop "Spooler" && net start "Spooler"
```

• Purpose: Stops and restarts a service.

• When to Use: When troubleshooting issues with services like printing, networking, or updates.

Disk & File System Checks

14\. Check Disk Health

```
chkdsk C:
```

• Purpose: Checks for disk errors.

• When to Use: When a system experiences slow performance or file corruption.

\


15\. Check Disk Space

```
wmic logicaldisk get size,freespace,caption
```

• Purpose: Displays available and used disk space.

• When to Use: When diagnosing storage-related issues.

\


16\. List Installed Programs

```
wmic product get name,version
```

• Purpose: Lists installed applications.

• When to Use: When identifying installed software or troubleshooting software issues.

\


17\. Check for Corrupt System Files

```
sfc /scannow
```

• Purpose: Scans and repairs system files.

• When to Use: When resolving missing or corrupt system file errors.

\


18\. Check and Repair Windows Image

```
DISM /Online /Cleanup-Image /RestoreHealth
```

• Purpose: Repairs Windows system image.

• When to Use: When sfc /scannow fails to resolve corruption issues.

User & Permissions Management

19\. List User Accounts

```
net user
```

• Purpose: Displays all user accounts.

• When to Use: When managing user accounts or checking for unauthorized users.

\


20\. Check Group Memberships for a User

```
net user username
```

• Purpose: Lists user group memberships.

• When to Use: When verifying user permissions.

\


21\. Reset a User’s Password

```
net user username newpassword
```

• Purpose: Resets a user’s password.

• When to Use: When a user forgets their password.

\


22\. Enable/Disable a User Account

```
net user username /active:yes
```

```
net user username /active:no
```

• Purpose: Enables or disables an account.

• When to Use: When managing user access.

Startup & Performance

23\. View Startup Programs

```
wmic startup get caption,command
```

• Purpose: Lists startup programs.

• When to Use: When identifying and disabling unnecessary startup programs.

\


24\. Check Boot Configuration

```
bcdedit
```

• Purpose: Displays boot settings.

• When to Use: When troubleshooting boot issues.

\


25\. Enable Safe Mode on Next Reboot

```
bcdedit /set {current} safeboot minimal
```

• Purpose: Forces next boot into Safe Mode.

• When to Use: When troubleshooting system instability.

Event Logs & System Monitoring

26\. View Recent System Errors

```
wevtutil qe System /c:10 /f:text /rd:true
```

• Purpose: Retrieves recent system errors.

• When to Use: When diagnosing crashes or system errors.

\


27\. Monitor Live System Events

```
eventvwr
```

• Purpose: Opens Event Viewer.

• When to Use: When investigating detailed logs.

Windows Update & Remote Admin Tasks

28\. Check for Windows Updates

```
wuauclt /detectnow
```

• Purpose: Forces Windows to check for updates.

\


29\. Restart Windows Update Service

```
net stop wuauserv && net start wuauserv
```

• Purpose: Restarts the Windows Update service.

\


30\. Enable Remote Desktop

```
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```

• Purpose: Enables Remote Desktop access.

These commands are essential for IT technicians to quickly diagnose and fix Windows issues. Let me know if you need additional details! 🚀
