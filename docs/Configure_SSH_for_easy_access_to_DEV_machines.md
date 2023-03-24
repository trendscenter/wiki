---
layout: default
title: Configure SSH for easy access to DEV machines
nav_order: 4
parent: Getting Started
last_modified_date: 10/2/2022 12:58
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

Create an SSH config file like below and save in `~/.ssh/config` file. 
On Windows machines, `~` corresponds to `C:\Users\<your_name>\` directory, so you should create the file `C:\Users\<your_name>\.ssh\config`.
Note that the file name does not have any extension like `.txt`.  

{: .tip}
Replace `<campusid>` with your GSU username in all the commands/configs below.

```
# for dev node access
host {{site.data.trends.dev_alias}}
	hostname {{site.data.trends.dev_node}}
	user <campusid>

# for login node/SLURM access
Host {{site.data.trends.login_alias}}
    HostName {{site.data.trends.login_alias}}
    User <campusid>
    ForwardAgent yes
    CertificateFile ~/.ssh/id_<campusid>-cert.pub
    IdentityFile ~/.ssh/id_<campusid>
```

Now run the following command to create SSH keys:

```
$ ssh-keygen -t ed25519 -f id_<campusid>
```

On Mac, add the key to your `ssh-agent`:

```
ssh-add -K ~/.ssh/id_<campusid>
```
It may complain that the option is deprecated, in which case try this instead:
```
ssh-add --apple-use-keychain ~/.ssh/id_<campusid>
```

Copy the key to the server:

```
$ ssh-copy-id -i id_<campusid> {{site.data.trends.login_alias}}
```

{: .tip}
If `ssh-copy-id` is not available in your local machine, open the file `~/.ssh/authorized_keys` on the cluster manually, and append the content of your public key `~/.ssh/id_rsa.pub` on your local machine to it.

Test the configuration, you should now be able to login without having to type password:

```
$ ssh -XY {{site.data.trends.dev_alias}}
$ ssh -XY {{site.data.trends.login_alias}}
```

## Forwarding a port (tunneling)

Update the ssh config like below to forward a port:

```
host {{site.data.trends.dev_alias}}
    HostName {{site.data.trends.dev_node}}
    user <campusID>
    LocalForward <port> localhost:<port>
```

## Remote coding in Visual Studio Code

Install [VS Code](https://code.visualstudio.com/) and then the [Remote Development plugin](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack).
Make sure the above configuration is working. Then go to the "Remote Explorer" tab to the left panel of VS Code and connect to `{{site.data.trends.dev_alias}}`.

