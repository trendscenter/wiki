---
layout: default
title: Helpful commands
nav_order: 6
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

### VPN address

`secureaccess.gsu.edu`

### SSH to the login node

`$ ssh -X `<CampusID>`@trendslogin.gsu.edu`
`$ ssh -Y `<CampusID>`@trendslogin.gsu.edu`

### Start interactive mode/terminal/bash on worker/compute nodes

*can be run on the login node*

`# Start interactive mode on a general-purpose compute node`
`$ srun -p qTRD -A PSYC0002 -v -n1 --mem=10g --pty /bin/bash    `

`# Start interactive mode on a GPU worker node`
`$ srun -p qTRDGPUH -A PSYC0002 -v -n1 --pty --mem=10g --gres=gpu:v100:1 /bin/bash`

`# Start interactive mode on a high-memory worker node`
`$ srun -p qTRDHM -A PSYC0002 -v -n1 --mem=10g --pty /bin/bash`

`# Start interactive mode on a general-purpose compute node with X11 GUI support`
`$ srun -p qTRD -A PSYC0002 -v -n1 --mem=10g --pty --x11 /bin/bash`

### Available modules (software)

*can be run on any node*

`$ module avail`

`# Search for a particular module`
`$ module avail 2>&1 | grep -i matlab`

`# load a particular module`
`$ module load Framework/Matlab2019b`

`# List loaded modules`
`$ module list`

`# Unload all modules`
`$ module purge`

### Info about the resources (queues, nodes and status) available

**Online:** <http://hpcstats.rs.gsu.edu/ganglia/?c=Trends>

### From terminal on the login node:

`$ sinfo`
`$ sinfo -o "%24n %7P %.11T %.4c %.8m %14C %10e"`
`$ sinfo -O "nodehost:16,partition:.8,cpus:.8,memory:.8,cpusstate:.16,freemem:.8,gres:.16,gresused:.16,statelong:.8,time:.16"`

### Find path to Matlab

*can be run on any node, but do not actually run `matlab` on the login node, please.*

`$ module load Framework/Matlab2019b`
`$ which matlab`

### Run software GUI

Method 1 (via SLURM X11):

`$ module load Framework/Matlab2019b`
`$ srun -p qTRD -A PSYC0002 -v -n1 --mem=10g --export=TERM,HOME --pty --x11 /apps/Framework/MATLAB/R2019b/bin/matlab`

Method 2 (via interactive mode):

`$ srun -p qTRD -A PSYC0002 -v -n1 --mem=10g --pty --x11 /bin/bash `
`$ module load Framework/Matlab2019b`
`$ matlab &`

### Edit files

*can be run on any node*

`$ nano `<filename>
`$ vi `<filename>

### Transfer files

`# from local to cluster`
`$ scp `<local path to file>` `<campusID>`@trendslogin.gsu.edu:`<server path>

`# from cluster to local`
`$ scp `<campusID>`@trendslogin.gsu.edu:`<server path>` `<local path to file>

### Submit a job to the scheduler

*can be run on the login node*

`# Submit a job script `
`$ sbatch JobSubmit.sh`

`# Submit a job array script`
`$ sbatch –array=1-5000%100 JobSubmit.sh`

### Sample SBATCH script

*For submitting jobs to the cluster*

<https://slurm.schedmd.com/sbatch.html>

`#!/bin/bash`
`#SBATCH -N 1`
`#SBATCH -n 1`
`#SBATCH --mem=10g`
`#SBATCH -p qTRD`
`#SBATCH -t 1440`
`#SBATCH -J `<job name>
`#SBATCH -e error%A.err`
`#SBATCH -o out%A.out`
`#SBATCH -A PSYC0002`
`#SBATCH --mail-type=ALL`
`#SBATCH --mail-user=`<email address>
`#SBATCH --oversubscribe`

`sleep 10s`

`export OMP_NUM_THREADS=1`
`export MODULEPATH=/apps/Compilers/modules-3.2.10/Debug-Build/Modules/3.2.10/modulefiles/`
`echo $HOSTNAME >&2`

`module load Framework/Matlab2019b`
`matlab -batch 'simple_example'`

`sleep 30s`

### Sample SBATCH (array) script

*For creating job arrays*

<https://slurm.schedmd.com/job_array.html>

`#!/bin/bash`
`#SBATCH -N 1`
`#SBATCH -n 1`
`#SBATCH --mem=10g`
`#SBATCH -p qTRD`
`#SBATCH -t 1440`
`#SBATCH -J `<job name>
`#SBATCH -e error%A-%a.err`
`#SBATCH -o out%A-%a.out`
`#SBATCH -A PSYC0002`
`#SBATCH --mail-type=ALL`
`#SBATCH --mail-user=`<email address>
`#SBATCH –oversubscribe`

`sleep 10s`

`export OMP_NUM_THREADS=1`
`export MODULEPATH=/apps/Compilers/modules-3.2.10/Debug-Build/Modules/3.2.10/modulefiles/`
`echo $HOSTNAME >&2`

`module load Framework/Matlab2019b`
`matlab -batch 'array_example($SLURM_ARRAY_TASK_ID)'`

`sleep 30s`

### Controlling jobs (to be run on the login node)

`# Check status of all jobs`
`$ squeue`

`# Check status of jobs by user`
`$ squeue -u `<campusID>

`# Continuously check status of jobs`
`$ watch -n 10 squeue -u `<campusID>

`# Check job status by ID`
`$ squeue -j `<jobID>

`# Cancel job by ID`
`$ scancel `<jobID>

### Login to a DEV node

*can be run on the login node, for lightweight experiments only*

`$ ssh -X trendscn019.rs.gsu.edu`
`$ ssh -X trendscn020.rs.gsu.edu`

### Start GUI application on DEV node

*can be run on a DEV node or in interactive mode only*

`$ module load Framework/Matlab2019b`
`$ matlab &`

### Set CPU affinity

`numactl --localalloc matlab -batch "myscript.m"`