---
layout: default
title: Helpful commands
nav_order: 6
parent: Getting Started
last_modified_date: 10/2/2022 13:01
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

### VPN address

`secureaccess.gsu.edu`

### SSH to the login node

```
$ ssh -X <CampusID>@{{site.data.trends.login_alias}}
```

### Start interactive mode/terminal/bash on worker/compute nodes

Can be run on the login node
{: .label .label-purple }

```
# Start interactive mode on a general-purpose compute node
$ srun -p qTRD -A <slurm_account_code> -v -n1 --mem=10g --pty /bin/bash    

# Start interactive mode on a GPU worker node
$ srun -p qTRDGPUH -A <slurm_account_code> -v -n1 --pty --mem=10g --gres=gpu:V100:1 /bin/bash

# Start interactive mode on a high-memory worker node
$ srun -p qTRDHM -A <slurm_account_code> -v -n1 --mem=10g --pty /bin/bash
```

### Available modules (software)

Can be run on any node
{: .label .label-purple }

```
$ module avail

# Search for a particular module
$ module avail matlab

# load a particular module
$ module load matlab/R2022a

# List loaded modules
$ module list

# Unload all modules
$ module purge
```

### Info about the resources (queues, nodes and status) available

#### Online
<https://arcxdmod.rs.gsu.edu/>

#### From terminal on the login node:

```
$ sinfo
$ sinfo -o "%24n %7P %.11T %.4c %.8m %14C %10e"
$ sinfo -O "nodehost:16,partition:.8,cpus:.8,memory:.8,cpusstate:.16,freemem:.8,gres:.16,gresused:.16,statelong:.8,time:.16"
```
### Find path to Matlab

Can be run on any node, but do not actually run matlab on the login node, please.
{: .label .label-purple }

```
$ module load matlab/R2022a
$ which matlab
```

### Run software GUI

From [https://hemera.rs.gsu.edu/](https://hemera.rs.gsu.edu/)

### Edit files

Can be run on any node
{: .label .label-purple }

```
$ nano <filename>
$ vi <filename>
```

### Transfer files

```
# from local to cluster
$ scp -r <local path to file> <campusID>@{{site.data.trends.login_alias}}:<server path>

# from cluster to local
$ scp -r <campusID>@{{site.data.trends.login_alias}}:<server path> <local path to file>
```

### Submit a job to the scheduler

Can be run on the login node
{: .label .label-purple }

```
# Submit a job script 
$ sbatch JobSubmit.sh

# Submit a job array script
$ sbatch –array=1-5000%100 JobSubmit.sh
```

### Sample SBATCH script

Please see [example SLURM scripts](Example_SLURM_scripts).

### Controlling jobs (to be run on the login node)

```
# Check status of all jobs
$ squeue

# Check status of jobs by user
$ squeue -u <campusID>

# Continuously check status of jobs
$ watch -n 10 squeue -u <campusID>

# Check job status by ID
$ squeue -j <jobID>

# Cancel job by ID
$ scancel <jobID>
```

### Login to a DEV node

Can be run on the login node/local machine, for lightweight experiments only
{: .label .label-purple }

```
$ ssh {{site.data.trends.dev_alias}}
```

### Set CPU affinity

`numactl --localalloc matlab -batch "myscript.m"`