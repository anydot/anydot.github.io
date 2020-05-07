---
title: "Powershell profile"
date: 2020-05-07T13:33:41+02:00
---

Powershell profile
<!--more-->
``` posh
Set-Alias -Name subl -Value "$Env:ProgramFiles\Sublime Text 3\subl.exe"
Set-PSReadlineKeyHandler -Key Tab -Function Complete
Set-PSReadlineKeyHandler -Key Ctrl+d -Function DeleteCharOrExit

Import-Module Posh-Git
```