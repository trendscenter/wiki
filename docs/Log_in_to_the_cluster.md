---
layout: default
title: Log in to the cluster
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

Please go through [https://arcwiki.rs.gsu.edu/en/home/ssh/signing-in](https://arcwiki.rs.gsu.edu/en/home/ssh/signing-in) to know more details about connecting to the cluster.

### VPN

You must be connected to the [GSU VPN](Configure_VPN), or in the GSU network to log in to the cluster. 

### Active allocation

[Request an account](Request_an_account).

### SSH keypair

Generate an SSH keypair in your local machine:

```
$ mkdir ~/.ssh
$ cd ~/.ssh
$ ssh-keygen -f id_<campusid>
```

make sure to use a [strong password](https://www.cisa.gov/secure-our-world/require-strong-passwords) when creating your keys!

### Signed public key

```
# copy the content of your public key
$ cat ~/.ssh/id_<campusid>.pub
### copy the output ###
```

Go to [https://elpis.rs.gsu.edu/](https://elpis.rs.gsu.edu/), then go to the "Sign SSH Certificate" page.
Here, paste the content of the public key and click "Sign Key".
If there is an error generating the certificate, please verify that you copied the public key contents correctly.
Download the generated certificate to your local machine and save in the `~/.ssh` folder.

```
$ mv ~/Downloads/id_<campusid>-cert.pub ~/.ssh
```

### Certificate Has An Expiration Date

If it's been about 3 months since you signed your certificate and authentication suddenly returns `username@arclogin.rs.gsu.edu: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).`. Your certificate may have expired. See description of this case in [the elpis documentation](https://arcwiki.rs.gsu.edu/en/home/ssh/authentication-issues). You can check via `ssh-keygen -L -f ~/.ssh/id_username-cert.pub`. This should return something like
```
❯ ssh-keygen -L -f .\.ssh\id_username-cert.pub
.\.ssh\id_cchildress-cert.pub:
        Type: ssh-ed25519-cert-v01@openssh.com user certificate
        Public key: ED25519-CERT SHA256:BmEP/qyJnwkJJDlFX3PcKav8zj1hMkam98h+JQLhtA0
        Signing CA: RSA SHA256:RkvuiBi72zpO9p5RfhKCgyVgTj+D+4nkQX62wY4UVR0 (using rsa-sha2-512)
        Key ID: "vault-clientrole-token-elpis-acids-06610ffeac899f09092439455f73dc29abfcce3d613246a6f7c87e2502e1b40d"
        Serial: 16511806482349416608
        Valid: from 2022-11-23T10:11:55 to 2023-02-21T10:12:25
        Principals:
                username
        Critical Options: (none)
```
Window's users have to hit <kbd>TAB</kbd> to resolve ~ to their home directory.
You want to check the valid dates to ensure the certificate is still valid.

### What do to if your certificate has expired?
1. Go to https://elpis.rs.gsu.edu and paste your public key into the Sign SSH Form. [Full instructions](https://arcwiki.rs.gsu.edu/en/home/elpis/signing-keys)
2. Save your new certificate as ~/.ssh/id_username-cert.pub replacing your old certificate.
3. Re-add your ssh key and certificate to the ssh-agent `ssh-add ~/.ssh/id_username`


## Connect to the cluster using terminal

### Create SSH configuration file

Create a file `~/.ssh/config` with the following contents.

```
Host {{site.data.trends.login_alias}}
    HostName {{site.data.trends.login_node}}
    User <campusid>
    ForwardAgent yes
    CertificateFile ~/.ssh/id_<campusid>-cert.pub
    IdentityFile ~/.ssh/id_<campusid>
```

### Configure SSH authentication agent

On Linux/Mac, the SSH authentication agent should be running by default. 
Run the following command to add the generated SSH key to the agent.

```
ssh-add ~/.ssh/id_<campusid>
```

On Windows, you need administrator privilege to enable the service.
Open a PowerShell window as administrator and run the following command:

```
$ Set-Service -Name ssh-agent -StartupType Automatic -Status Running
```

Then you should be able to use the `ssh-add` command above.

If you do not have administrator access to your machine, please contact the administrator with the above information.

### Connect to the cluster login node

Run the following command to get connected to the cluster.

```
$ ssh {{site.data.trends.login_alias}}
[<campusID>@{{site.data.trends.login_prompt}} ~]$
```

{: .caution}
> ## Head/login node vs compute/worker nodes
> `@{{site.data.trends.login_prompt}}` indicates that you are connected to the head/login node. 
> On the login node you can submit jobs, interact with the cluster, edit files etc. 
> But you should not run lengthy computations (more than a few seconds) on the login node itself. 

For running computations, please allocate resources on a compute/worker node which are accessible from the head/login node:

```
[<campusID>@{{site.data.trends.login_prompt}} ~]$ srun -p qTRD -A <slurm_account_code> -v -n1 --mem=10g -t60 --pty /bin/bash
srun: defined options
srun: -------------------- --------------------
srun: account             : <slurm_account_code>
srun: mem                 : 10G
srun: ntasks              : 1
srun: partition           : qTRD
srun: pty                 : set
srun: time                : 01:00:00
srun: verbose             : 1
srun: x11                 : all
srun: -------------------- --------------------
srun: end of defined options
srun: Waiting for nodes to boot (delay looping 450 times @ 0.100000 secs x index)
srun: Nodes trendscn013.rs.gsu.edu are ready for job
 srun: jobid 376466: nodes(1):trendscn013.rs.gsu.edu', cpu counts: 1(x1) 
srun: CpuBindType=(null type)
srun: launching 376466.0 on host trendscn013.rs.gsu.edu, 1 tasks: 0
srun: route default plugin loaded
srun: Node trendscn013.rs.gsu.edu, 1 tasks started
[<campusID>@trendscn013 ~]$
```

The above command will allocate 1 CPU on one of the nodes under `qTRD` queue and 10GB of RAM on the said node (`trendscn013` in this case) for 60 minutes and start a `bash` session. 
See [this page](Cluster_queue_information) for more information about the available queues.

## Connect to the cluster using VNC

You can also connect to the cluster and GUI applications from [https://hemera.rs.gsu.edu/](https://hemera.rs.gsu.edu/).


