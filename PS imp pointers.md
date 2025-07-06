# command history:-
**PSReadLine** stores all the command history in a file called $($host.Name)_history.txt located at **$env:APPDATA\Microsoft\Windows\PowerShell\PSReadLine**.

# exploiting execution policy:-
https://www.netspi.com/blog/technical-blog/network-penetration-testing/15-ways-to-bypass-the-powershell-execution-policy/

# RSAT 
One requirement is to have the optional feature Remote System Administration Tools installed. This feature is the only way to get the official ActiveDirectory PowerShell module.
>Get-WindowsCapability -Name RSAT* -Online | Add-WindowsCapability -Online

# helpful directories in enumeration:-
-Looking in a Users \AppData\ folder is a great place to start. Many applications store configuration files, temp saves of documents, and more.

-A Users home folder C:\Users\User\ is a common storage place; things like VPN keys, SSH keys, and more are stored. Typically in hidden folders. (Get-ChildItem -Hidden)

-The Console History files kept by the host are an endless well of information, especially if you land on an administrator's host. You can check two different points:
	-C:\Users\<USERNAME>\AppData\Roaming\Microsoft\Windows\Powershell\PSReadline\ConsoleHost_history.txt
	-Get-Content (Get-PSReadlineOption).HistorySavePath

-Checking a user's clipboard may also yield useful information. You can do so with Get-Clipboard

-Looking at Scheduled tasks can be helpful as well.

# installing PowerView:-
**PS C:\> Invoke-WebRequest -Uri "https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Recon/PowerView.ps1" -OutFile "C:\PowerView.ps1"**
if Invoke-WebRequest is restricted, 
**PS C:\htb> (New-Object Net.WebClient).DownloadFile("https://github.com/BloodHoundAD/BloodHound/releases/download/4.2.0/BloodHound-win32-x64.zip", "Bloodhound.zip")**

# Scripting and Automation:-
Create dir in **$env:PSModulePath** so that it is easily found.
help should be written one line above the function.
**Export-ModuleMember** to specify which members to export.
