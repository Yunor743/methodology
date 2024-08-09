
Run **cmd.exe** then type *"powershell"*

Enter the following command:
```powershell
$LanguageList = Get-WinUserLanguageList
$LanguageList.Add("fr-FR")
Set-WinUserLanguageList $LanguageList
```

And select **yes** on the following prompt

<u>example:</u>

Then on the bottom of the screen select you language

![[Pasted image 20230909170111.png]]

> src : https://www.anoopcnair.com/best-ways-to-change-keyboard-layouts-windows-11

