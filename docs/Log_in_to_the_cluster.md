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
$ ssh-keygen -t ed25519 -f id_<campusid>
```

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
[<campusID>@{{site.data.trends.login_prompt}} ~]$ srun -p qTRD -A <slurm_account_code> -v -n1 --mem=10g -t60 --pty --x11 /bin/bash
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


