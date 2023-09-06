---
layout: default
title: Setting up WSL for Windows with VPN
nav_order: 2
parent: Getting Started
last_modified_date: 09/25/2022 9:29
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Prerequisites


To be able to ssh arclogin from Windows Subsystem for Linux (WSL) with GSU VPN turned on do the following steps:

### Power shell

Find Windows power shell in you start menu and choose “open file in location”.

Open “properties” of Windows Power Shell.

Click “Advanced” options. 

Check the box next to “Run as administrator” and Click “OK”.

Click “OK”.

### wsl_vpn.ps1 

Create a text file wsl_vpn.ps1 with the following text :

```
Write-Host "Script wsl_vpn.ps1 started."
Get-NetAdapter | Where-Object {$_.InterfaceDescription -Match "Cisco AnyConnect"} | Set-NetIPInterface -InterfaceMetric 4000
Get-NetIPInterface -InterfaceAlias "vEthernet (WSL)" | Set-NetIPInterface -InterfaceMetric 1
Write-Host "Script wsl_vpn.ps1 finished."
``` 
Create a new shortcut.  In the “Type the location of the item” browse the directory of  wsl_vpn.ps1.

Create a name of the shortcut wsl_vpn_shortcut.ps1 (or whatever you want).

### wsl_vpn_shortcut.ps1 properties

Open “properties” of wsl_vpn_shortcut.ps1
Add the text
```
powershell.exe -NoExit -ExecutionPolicy Bypass -File
``` 
in the very beginning of field “Target” and Apply this change.

Click “Advanced” options. 

Check the box next to “Run as administrator” and Click “OK”

Click “OK”

Put the file wsl_vpn_shortcut.ps1 in a convenient directory. 


### login to cluster

To login cluster from wls from vpn you need:

a) run GSU vpn

b) run WSL

с) run wsl_vpn_shortcut.ps1 
 

### Check up
After these steps you will be able to ssh arclogin.
 
To check that you made steps 1-2 correct print in wls:

```
ping 8.8.8.8 
```







