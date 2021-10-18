---
layout: default
title: Configure SSH for easy access to DEV machines
nav_order: 4
parent: Getting Started
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

-   Please follow this guide:
    <https://docs.google.com/document/d/1C3IK38d5XiEIafktjJ6LxXVFMrj77unXm_9VAjGe3Ww/edit?usp=sharing>
-   Annotated video:
    <https://www.dropbox.com/s/ue1g0i24kpaco4g/setting_up_ssh_vscode_remote_matlab_editing_executing.mp4?dl=0>

## Setting up SSH configuration

The following should be set up on a local machine.

Create an SSH config file like below and save in `~/.ssh/config` file:

```
host trendslogin
   HostName trendslogin.gsu.edu
   user <campusID>

host devtrends01
   HostName trendscn017.rs.gsu.edu
   user <campusID>
   # ProxyCommand C:\\Windows\\System32\\OpenSSH\\ssh.exe -W -XY %h:%p trendslogin # on Windows, not needed anymore
   # ProxyJump trendslogin # on Unix, not needed anymore

host trendsgndev01
   HostName trendsgndev101.rs.gsu.edu
   user <campusID>
   # ProxyCommand C:\\Windows\\System32\\OpenSSH\\ssh.exe -W -XY %h:%p trendslogin # on Windows, not needed anymore
   # ProxyJump trendslogin # on Unix, not needed anymore

host devtrendsgpu
   HostName trendsagn019.rs.gsu.edu
   user <campusID>
   # ProxyCommand C:\\Windows\\System32\\OpenSSH\\ssh.exe -W -XY %h:%p trendslogin # on Windows, not needed anymore
   # ProxyJump trendslogin # on Unix, not needed anymore
```

Create SSH keys:

```
$ ssh-keygen -t rsa
```

Copy the key to the server:

```
$ ssh-copy-id trendslogin
```

If `ssh-copy-id` is not available in your local machine, open the file
`~/.ssh/authorized_keys` <i>on the cluster</i> manually, and append the
content of your public key `~/.ssh/id_rsa.pub` <i>on your local
machine</i> to it.

Test the configuration, you should now be able to login without having
to type password:

```
$ ssh -XY trendslogin
$ ssh -XY devtrends01
$ ssh -XY trendsgndev01
$ ssh -XY trendsgndev02
```

## Remote coding in Visual Studio Code

Install [VS Code](https://code.visualstudio.com/) and then the [Remote
Development
plugin](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack).
Make sure the above configuration is working. Then go to the "Remote
Explorer" tab to the left panel of VS Code and connect to `devtrends01`.

Please go through the above annotated video to see how to open folders
and files, edit/debug code, run those from console and/or submit jobs on
the cluster, inspect output files and figures in VS Code.