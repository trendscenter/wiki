---
layout: default
title: Configure WSL
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

### Enable Windows Features
From the start menu, search for "Turn Windows Features On and Off".

Click to enable the check box next to "Virtual Machine Platform" to turn it on. 

Click to enable the check box next to "Windows Subsystem for Linux" to turn it on. 

Click OK and  you will be prompted to restart the computer. 

### Download Linux Distribution from App Store
From the start menu, open the Microsoft Store and type "Windows Subsystem for Linux".

From here you can install the Linux distribution that you want, it should say "Windows Subsystem for Linux" in the app description. 

### Open the WSL App and Install SSH
From the start menu, type the name of the Linux distribution and you can open the WSL terminal by clicking on the app icon. 

If you are using a Debian based Linux distribution, use the following command in the WSL terminal to install SSH. If you are using a Linux distribution that doesn't have the apt package manager, then use the package manager specific to your Linux distribution to install SSH if necessary.
```
sudo apt-get install ssh
```
### Make and Configure SSH Keys on WSL
Move to your home directory, create your ssh folder, and move into the ssh folder. Create the config file, make sure it is not called `config.txt`.
```
cd ~
mkdir .ssh
cd .ssh
touch config
```

Update your `~/.ssh/config` file to read the following. Note that all instances of `<campusid>` should be replaced with your GSU username.

    host arctrdgndev101
    	hostname arctrdgndev101.rs.gsu.edu
    	user <campusid>

    Host arclogin
        HostName arclogin
        User <campusid>
        ForwardAgent yes
        CertificateFile ~/.ssh/id_<campusid>-cert.pub
        IdentityFile ~/.ssh/id_<campusid>

Now issue the following command to generate your key.
```
$ ssh-keygen -t ed25519 -f id_<campusid>
```

Next, type the following command to enable the ssh-agent service.
```
eval "$(ssh-agent)"
```

Type the following command to add your key.
```
ssh-add ~/.ssh/id_<campusid>
```


Go to [https://elpis.rs.gsu.edu/](https://elpis.rs.gsu.edu/), then go to the "Sign SSH Certificate" page. Here, paste the content of the public key and click "Sign Key". If there is an error generating the certificate, please verify that you copied the public key contents correctly. Since WSL is a virtual machine and is isolated from your local files, copy the contents of the certificate onto the clipboard. Use vim or nano to create a new file called `id_<campusid>-cert.pub` and paste the contents of the certificate into here. Write and save the file. 

Type the following command: 
```
ssh arclogin
```
If you are connected to the GSU VPN, then use the following steps to ssh to the cluster. 

### Fix DNS Issues on WSL
Up to this point, if you're working from the GSU network, it appears that SSH to the cluster in WSL works. If you want to SSH to the cluster from WSL while connected to the GSU VPN, there are some issues that prevent it. This wsl-vpnkit script can be used to run on the side to resolve DNS issues in WSL. This software should allow SSH while on the VPN to work. Follow the steps below. 


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


### Login to cluster

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

Now at the WSL prompt, type `ssh arclogin` to verify that you can ssh to the cluster while connected to the GSU VPN.






