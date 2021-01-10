---
title: "Powershell profile"
date: 2020-05-07T13:33:41+02:00
---

Powershell profile - updated 2021/01/10
<!--more-->
``` posh
$global:promptPrefix = "PS"

Set-Alias -Name subl -Value "$Env:ProgramFiles\Sublime Text 3\subl.exe"
Set-PSReadlineKeyHandler -Key Tab -Function Complete
Set-PSReadlineKeyHandler -Key Ctrl+d -Function DeleteCharOrExit

function ADO
{
    $global:promptPrefix = "ADO"
    Set-Location C:\dev\ado\src
    .\init.ps1 -KeepPsReadLine $true
    $ENV:VSInstanceVersion = 16
    $ENV:EnableHardLinksDuringBuild = "true" # enable MSBuild optimization
}

function prompt
{
    $prompt = "$global:promptPrefix $($executionContext.SessionState.Path.CurrentLocation)$('>' * ($nestedPromptLevel + 1)) ";
    $Host.UI.RawUI.WindowTitle = $prompt;
    return $prompt;
}
```