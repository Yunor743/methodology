
`gpedit.msc` is used to manage local group policies, 

Indeed, if you search for the local Group Policy Editor or the corresponding file name "gpedit.msc", you'll see that Windows 10 and 11 Home Edition don't have this feature.

![[Pasted image 20231214115057.png]]

To do this, open a command prompt (cmd.exe) as administrator.

```powershell
FOR %F IN ("%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~*.mum") DO (DISM /Online /NoRestart /Add-Package:"%F")
FOR %F IN ("%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~*.mum") DO (DISM /Online /NoRestart /Add-Package:"%F")
```

As you can see, these 2 commands are used to install these packages:

- `Microsoft-Windows-GroupPolicy-ClientTools-Package~*.mum`
- `Microsoft-Windows-GroupPolicy-ClientExtensions-Package~*.mum`

---

Source:

- https://www.informatiweb.net/tutoriels/informatique/windows/windows-10-11-ajouter-l-editeur-de-gpo-gpedit-msc-sous-windows-famille.html