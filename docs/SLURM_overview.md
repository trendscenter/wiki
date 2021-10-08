---
layout: default
title: SLURM Overview
nav_order: 4
has_children: true
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Overview

The TReNDS cluster uses SLURM workload manager. From
<https://slurm.schedmd.com/quickstart.html>:

> Slurm is an open source, fault-tolerant, and highly scalable cluster
> management and job scheduling system for large and small Linux
> clusters. As a cluster workload manager, Slurm has three key
> functions.
>
> -   First, it allocates exclusive and/or non-exclusive access to
>     resources (compute nodes) to users for some duration of time so
>     they can perform work.
> -   Second, it provides a framework for starting, executing, and
>     monitoring work (normally a parallel job) on the set of allocated
>     nodes.
> -   Finally, it arbitrates contention for resources by managing a
>     queue of pending work.

## Example commands

### `sinfo`: What partitions exist on the system

```
[msalman@trendslogin01 ~]$ sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
qTRD         up 5-08:00:00      3    mix trendscn001.rs.gsu.edu,trendscn004.rs.gsu.edu,trendscn008.rs.gsu.edu
qTRD         up 5-08:00:00      7  alloc trendscn010.rs.gsu.edu,trendscn011.rs.gsu.edu,trendscn012.rs.gsu.edu,trendscn013.rs.gsu.edu,trendscn014.rs.gsu.edu,trendscn015.rs.gsu.edu,trendscn016.rs.gsu.edu
qTRD         up 5-08:00:00      6   idle trendscn002.rs.gsu.edu,trendscn003.rs.gsu.edu,trendscn005.rs.gsu.edu,trendscn006.rs.gsu.edu,trendscn007.rs.gsu.edu,trendscn009.rs.gsu.edu
qTRDEV       up 5-02:00:00      2   idle trendscn019.rs.gsu.edu,trendscn020.rs.gsu.edu
qTRDHM       up 5-08:00:00      3   idle trendsmn001.rs.gsu.edu,trendsmn002.rs.gsu.edu,trendsmn003.rs.gsu.edu
qTRDGPUH     up 5-08:00:00      1  alloc trendsgn001.rs.gsu.edu
qTRDGPUH     up 5-08:00:00      1   idle trendsgn002.rs.gsu.edu
qTRDGPUL     up 1-00:00:00      1  alloc trendsgn001.rs.gsu.edu
qTRDGPUL     up 1-00:00:00      1   idle trendsgn002.rs.gsu.edu
```

The example shows the following:

-   There are 5 partitions: qTRD, qTRDEV, qTRDHM, qTRDGPUH and qTRDGPUL.
-   All partitions are in UP state.
-   In the general-purpose compute queue qTRD, trendscn001.rs.gsu.edu is
    in mixed state, meaning some of its CPUs are allocated while others
    are idle.
-   trendscn0\[10-16\].rs.gsu.edu are all fully allocated, while
    trendscn00\[2,3,5,6,7,9\].rs.gsu.edu are idle.
-   In the high-memory compute queue qTHDHM, nodes
    trendsmn0\[01-03\].rs.gsu.edu are all in idle state.
-   In the GPU compute queues, trendsgn001.rs.gsu.edu is fully allocated
    whereas trendsgn002.rs.gsu.edu is idle.

`sinfo` command has many options to view more detail information:
<https://slurm.schedmd.com/sinfo.html>

### `squeue`: What jobs exist on the system

The ST field is the job state. All the jobs are in a running state (R is
an abbreviation for Running). One job is in a pending state (PD is an
abbreviation for Pending). The TIME field shows how long the jobs have
run for using the format days-hours:minutes:seconds. The
NODELIST(REASON) field indicates where the job is running or the reason
it is still pending. Typical reasons for pending jobs are Resources
(waiting for resources to become available) and Priority (queued behind
a higher priority job).

```
[msalman@trendslogin01 ~]$ squeue
            JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
376056_[401-3110%4     qTRD   airaji   airaji PD       0:00      1 (JobArrayTaskLimit)
           374007      qTRD  jchen84  jchen84  R 1-13:54:30      1 trendscn008.rs.gsu.edu
           374001      qTRD  jchen84  jchen84  R 1-13:55:00      1 trendscn008.rs.gsu.edu
           341999      qTRD     bash    kduan  R 4-12:46:16      1 trendscn012.rs.gsu.edu
           340583      qTRD     bash  jfries1  R 5-00:22:49      1 trendscn012.rs.gsu.edu
           357922    qTRDHM     bash     lwu9  R 2-11:03:01      1 trendsmn001.rs.gsu.edu
           376467      qTRD     bash  jfries1  R      35:11      1 trendscn013.rs.gsu.edu
      370623_2896    qTRDHM   airaji   airaji  R 1-11:52:52      1 trendsmn002.rs.gsu.edu
      370623_2890    qTRDHM   airaji   airaji  R 1-11:53:25      1 trendsmn002.rs.gsu.edu
      370623_2845    qTRDHM   airaji   airaji  R 1-11:57:26      1 trendsmn002.rs.gsu.edu
       376056_302      qTRD   airaji   airaji  R   14:59:23      1 trendscn009.rs.gsu.edu
       376056_303      qTRD   airaji   airaji  R   14:59:23      1 trendscn009.rs.gsu.edu
       376056_304      qTRD   airaji   airaji  R   14:59:23      1 trendscn009.rs.gsu.edu
        370623_75    qTRDHM   airaji   airaji  R 1-16:38:16      1 trendsmn002.rs.gsu.edu
        370623_78    qTRDHM   airaji   airaji  R 1-16:38:16      1 trendsmn002.rs.gsu.edu
           356439    qTRDHM     bash     lwu9  R 2-13:29:43      1 trendsmn001.rs.gsu.edu
```

`squeue` command has many options to view more detail information:
<https://slurm.schedmd.com/squeue.html>

### `srun`: Create a resource allocation and launch the tasks for a job step

Running the following command will launch bash/shell in a compute node.

```
[campusID@trendslogin01 ~]$ srun -p qTRD -A PSYC0002 -v -n1 --mem=10g --pty --x11 /bin/bash
srun: defined options
srun: -------------------- --------------------
srun: account             : PSYC0002
srun: mem                 : 10G
srun: ntasks              : 1
srun: partition           : qTRD
srun: pty                 : set
srun: verbose             : 1
srun: x11                 : all
srun: -------------------- --------------------
srun: end of defined options
srun: Waiting for nodes to boot (delay looping 450 times @ 0.100000 secs x index)
srun: Nodes trendscn001.rs.gsu.edu are ready for job
srun: jobid 4011166: nodes(1):`trendscn001.rs.gsu.edu', cpu counts: 1(x1)
srun: CpuBindType=(null type)
srun: launching 4011166.0 on host trendscn001.rs.gsu.edu, 1 tasks: 0
srun: route default plugin loaded
srun: Node trendscn001.rs.gsu.edu, 1 tasks started
[campusID@trendscn001 ~]$
```

**Explanation**:
- `-p qTRD`: partition to run job on. See [Cluster & queue information](Cluster_queue_information) page for more information
- `-A PSYC0002`:  user group. See [Request an account](Request_an_account) page for list of groups
- `-v`: verbose mode
- `-n1`: number of tasks to run. Set to 1 unless needed. See [Granular resource allocation with srun](Example_SLURM_scripts#granular-resource-allocation-with-srun) for example.
- `--mem=10g`: amount of memory requested (10 gigabytes)
- `--pty`: executes task in pseudo terminal mode
- `--x11`: sets up X11 forwarding (for GUI applications)
- `/bin/bash`: the program to run, in this case `bash`

After running the command, observe the output to see if what you requested is actually allocated (under `defined options`). Notice the last line `srun: Node trendscn001.rs.gsu.edu, 1 tasks started`, which means the task started successfully on a compute node `trendscn001.rs.gsu.edu`, hence the prompt has changed to `campusID@trendscn001`. Otherwise if there is an error, observe the output for possible reasons.

The following command launches Matlab GUI in a compute node in the qTRD
partition, allocates 1 cpu and 10GB memory.

```
$ module load Framework/Matlab2019b
$ srun -p qTRDEV -A PSYC0002 -v -n1 -c1 --mem=10g --pty --x11 /apps/Framework/MATLAB/R2019b/bin/matlab
```

`srun` command has many options available to control what resource are
allocated and how tasks are distributed across those resources:
<https://slurm.schedmd.com/srun.html>