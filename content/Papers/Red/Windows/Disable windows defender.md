## How to disable windows Defender:

##### Warning
After disabling the AV, Windefender (if activated) can detect the misconfiguration and automatically heal (repair) itself:
see https://www.microsoft.com/en-us/wdsi/threats/malware-encyclopedia-description?name=VirTool%3aWin32%2fDefenderTamperingRestore&threatid=2147741622


## Method 1 : (Via powershell)

> warnings:
> - Need high privileges
> - victim will receive a notification that the protection was disabled
> - This technique is blocked if "tamper protection" is active: https://stackoverflow.com/questions/60035145/powershell-set-mppreference-disablerealtimemonitoring-true-not-working

To display a list of cmdlets contained in the Defender module, run the following command: `Get-Command -Module Defender`
```powershell
# Check if windows Defender srvice is running
Get-Service Windefend, SecurityHealthService, wscsvc| Select Name,DisplayName, Status
# Get windows Defender status : enabled options, virus definition date and version, last scan time, and others.
Get-MpComputerStatus
# Get a list of the disable options
Get-MpPreference | fl disable*
# Disable Windows Defender (Need high privilege)
Set-MpPreference -DisableRealtimeMonitoring $true
# Disable everything
Set-MpPreference -DisableIntrusionPreventionSystem $true -DisableIOAVProtection $true -DisableRealtimeMonitoring $true -DisableScriptScanning $true -EnableControlledFolderAccess Disabled -EnableNetworkProtection AuditMode -Force -MAPSReporting Disabled -SubmitSamplesConsent NeverSend
# To completely disable Windows Defender on a computer
New-ItemProperty -Path “HKLM:\SOFTWARE\Policies\Microsoft\Windows Defender” -Name DisableAntiSpyware -Value 1 -PropertyType DWORD -Force
# Disabling via group policies
# see : https://wethegeek.com/how-to-disable-windows-defender-in-windows-10/

```

##### Other (possible) interesting registry keys:
- `HKLM:\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection` => `DisableRealtimeMonitoring`
- `HKLM:\SOFTWARE\Microsoft\Windows Defender` => `DisableAntiSpyware`

> "There is not option to disable “Tamper Protection” in powershel (that’s the point ….)."
> see https://bidouillesecurity.com/disable-windows-defender-in-powershell/

> Resources : https://theitbros.com/managing-windows-defender-using-powershell/


## Method 2 (via script)
> Warning : Noisy and GUI alert

##### TL;DR
The final script can be found here : [https://github.com/jeremybeaume/tools/blob/master/disable-defender.ps1](https://github.com/jeremybeaume/tools/blob/master/disable-defender.ps1)

> Resource: https://bidouillesecurity.com/disable-windows-defender-in-powershell/


---
## Method 3 (via GUI) (work well !) and group policies (GPO)
> Instructions from the Commando-VM installation procedure


In newer versions of Windows, Group Policy settings for Microsoft Defender are reverted back.  
To prevent this, _before_ changing them:

1. Open Resource Monitor (type `resmon.exe` in the search box)
2. Overview
3. Find `MsMpEng.exe` in the list
4. Right-click > `Suspend Process`

In Windows versions 1909 and higher, Tamper Protection was added. **Tamper Protection must be disabled, otherwise Group Policy settings are ignored.**

1. Open Windows Security (type `Windows Security` in the search box)
2. Virus & threat protection > Virus & threat protection settings > Manage settings
3. Switch `Tamper Protection` to `Off`

> **Important.** Tamper Protection must be disabled before changing Group Policy settings.

Depending on your windows version and type, you will need to install `gpedit.msg` : [[Group Policies (GPO)]]

##### To permanently disable Real Time Protection
1.  Open Local Group Policy Editor (type `gpedit.msc` in the search box)
2.  Computer Configuration > Administrative Templates > Windows Components > Microsoft Defender Antivirus > Real-time Protection
3.  Enable `Turn off real-time protection`

##### To permanently disable Microsoft Defender:
1.  Open Local Group Policy Editor (type `gpedit` in the search box)
2.  Computer Configuration > Administrative Templates > Windows Components > Microsoft Defender Antivirus
3.  Enable `Turn off Microsoft Defender Antivirus`

##### Disable Defender service : Scheduled checks
1. Go to the search bar and type: task scheduler and press Enter;  
2. Click the arrow next to Scheduler Library to expand the session and navigate to the following path:  `Microsoft \ Windows \ Windows Defender  `
3. Click on Windows Defender and a window with Defender services will appear;  
4. Right-click Windows Defender Schedule Scan and select Disable;

---

## Method 4 Safe mode

Some of the tricks shown before doesn't work anymore, 

Many Settings aren't allowed to change during the normal usage. It is neccessary to start Windows in the safe Mode, now you are safe to do all the *** Win does not allow. Just kidding be careful, like changes at the registry.

How to start safe mode?

1. Windows key + R
2. enter "msconfig"
3. Select boot tab
4. Check "Safe Mode" at boot options-Panel
5. Accept or OK and restart

Now all the changes mentioned before can be done. Same procedure to start windows in normal Mode but just uncheck "Safe Mode"

---

## Method 5 : Defender remover

Use a custom tool to remove defender:
- https://github.com/ionuttbara/windows-defender-remover
- https://github.com/swagkarna/Defeat-Defender

---

More resources:
- [John Hammond - Can you DISABLE Windows Defender Antivirus?](https://www.youtube.com/watch?v=HWck6-CnlX8)
- https://www.windowscentral.com/how-permanently-disable-windows-defender-windows-10
- https://answers.microsoft.com/en-us/windows/forum/all/how-to-turn-off-automatic-scan-setting/63be886f-b042-4895-a79b-345b0db5ca84
- https://superuser.com/questions/1757339/how-to-permanently-disable-windows-defender-real-time-protection-with-gpo/1757341#1757341
