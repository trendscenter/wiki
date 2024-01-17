---
layout: default
title: SLURM Overview
nav_order: 4
has_children: true
last_modified_date: 10/2/2022 15:36
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

```bash
bbaker43@arctrdlogin001:/data/users3/bbaker$ sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
qTRD         up 5-08:00:00      5    mix arctrdcn[001,004-005,008,010]
qTRD         up 5-08:00:00      1  alloc arctrdcn007
qTRD         up 5-08:00:00      6   idle arctrdcn[006,009,012,014-016]
qTRDEV       up 5-02:00:00      0    n/a
qTRDHM       up 5-08:00:00      2    mix arctrdhm[001-002]
qTRDHM       up 5-08:00:00      1   idle arctrdhm003
qTRDGPUH     up 5-08:00:00      3    mix arctrddgxa002,arctrdgn[001-002]
qTRDGPUH     up 5-08:00:00      2   idle arctrddgxa[001,003]
qTRDGPUM     up 5-08:00:00      3    mix arctrddgxa002,arctrdgn[001-002]
qTRDGPUM     up 5-08:00:00      2   idle arctrddgxa[001,003]
qTRDGPUL     up 5-08:00:00      3    mix arctrddgxa002,arctrdgn[001-002]
qTRDGPUL     up 5-08:00:00      2   idle arctrddgxa[001,003]
qTRDGPU      up 5-08:00:00     18    mix arctrdagn[001,003,031-046]
qTRDGPU      up 5-08:00:00     12   idle arctrdagn[002,004-010,014-017]
qTRDBF       up 5-08:00:00      2  alloc arctrdcn[019-020]
qTRDGPUBF    up 5-08:00:00      1   idle arctrdagn020
```

The example shows the following:

-   There are 7 primary partitions: `qTRD`, `qTRDEV`, `qTRDHM`, `qTRDGPU`, `qTRDGPUH`, `qTRDGPUM` and `qTRDGPUL`. In addition, there are two brainforge-specific partitions: `qTRDBF` and `qTRDGPUBF`.
-   All partitions are in `up` state.
-   In the general-purpose compute queue qTRD, arctrdcn[001,004-005,008,010].rs.gsu.edu are
    in a mixed state, meaning some of their CPUs are allocated while others
    are idle.
-   arctrdcn007.rs.gsu.edu is fully allocated, while
    arctrdcn\[006,009,012,014-016\].rs.gsu.edu are idle.

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

```bash
 bbaker43@arctrdlogin001:/data/users3/bbaker$ squeue
 JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
4295492      qTRD  test_cn  ppopov1 PD       0:00      1 (Resources)
4295347      qTRD     bash nlewis26  R   17:33:30      1 arctrdcn001
4296544      qTRD     bash hpetropo  R       6:35      1 arctrdcn001
4296526      qTRD     bash    mduda  R      33:00      1 arctrdcn001
4296498      qTRD     bash  jfries1  R    1:27:35      1 arctrdcn001
4296543    qTRDBF bf_UTD_A svc-brai PD       0:00      1 (Resources)
4296545    qTRDBF bf_UTD_A svc-brai PD       0:00      1 (Resources)
4296549    qTRDBF bf_UTD_A svc-brai PD       0:00      1 (Resources)
4296548    qTRDBF bf_UTD_A svc-brai PD       0:00      1 (Resources)
4296547    qTRDBF bf_UTD_A svc-brai PD       0:00      1 (Resources)
4296541    qTRDBF bf_UTD_A svc-brai  R      15:35      1 arctrdcn020
4296535    qTRDBF bf_A0011 svc-brai  R      22:55      1 arctrdcn020
4296536    qTRDBF bf_A0011 svc-brai  R      22:55      1 arctrdcn020
4296534    qTRDBF bf_A0011 svc-brai  R      23:13      1 arctrdcn020
4296531    qTRDBF bf_A0011 svc-brai  R      23:58      1 arctrdcn019
4296532    qTRDBF bf_A0011 svc-brai  R      23:58      1 arctrdcn019
4296533    qTRDBF bf_A0011 svc-brai  R      23:58      1 arctrdcn019
4296530    qTRDBF bf_A0011 svc-brai  R      24:18      1 arctrdcn019
4291821   qTRDGPU  cfrhwtr washbee1  R 2-14:48:59      1 arctrdagn032
4291822   qTRDGPU  cflhptr washbee1  R 2-14:48:59      1 arctrdagn033
4291823   qTRDGPU  cfrhptr washbee1  R 2-14:48:59      1 arctrdagn033
4291820   qTRDGPU  cflhwtr washbee1  R 2-14:49:18      1 arctrdagn031
```

`squeue` command has many options to view more detail information:
<https://slurm.schedmd.com/squeue.html>

### `srun`: Create a resource allocation and launch the tasks for a job step

Running the following command will launch bash/shell in a compute node.

```bash
bbaker43@arctrdlogin001:~$ srun -p qTRD -A <slurm_account_code> -v -c 4 --nodes=1 --ntasks-per-node=1 --mem=4G --time=1:00:00 --pty -J myInteractiveJob /bin/bash
srun: defined options
srun: -------------------- --------------------
srun: account             : <slurm_account_code>
srun: cpus-per-task       : 4
srun: job-name            : myInteractiveJob
srun: mem                 : 4G
srun: nodes               : 1
srun: ntasks-per-node     : 1
srun: partition           : qTRD
srun: pty                 : set
srun: time                : 01:00:00
srun: verbose             : 1
srun: -------------------- --------------------
srun: end of defined options
srun: job 4296558 queued and waiting for resources
srun: job 4296558 has been allocated resources
srun: Waiting for nodes to boot (delay looping 6150 times @ 0.100000 secs x index)
srun: Nodes arctrdcn001 are ready for job
srun: jobid 4296558: nodes(1):`arctrdcn001', cpu counts: 4(x1)
srun: Implicitly setting --exact, because -c/--cpus-per-task given.
srun: launch/slurm: launch_p_step_launch: CpuBindType=(null type)
srun: launching StepId=4296558.0 on host arctrdcn001, 1 tasks: 0
srun: route/default: init: route default plugin loaded
srun: launch/slurm: _task_start: Node arctrdcn001, 1 tasks started
(base) bbaker43@arctrdcn001:~$
```

**Explanation**:
- `-p qTRD`: partition to run job on. See [Cluster & queue information](Cluster_queue_information) page for more information
- `-A <slurm_account_code>`:  user group. See [Request an account](Request_an_account) page for list of groups
- `-v`: launch in verbose mode
- `-c 4`: the number of CPUs to use
- `--nodes 1 --ntasks-per-node=1`: number of nodes to use and tasks per node. Set both to 1 unless needed. See [Granular resource allocation with srun](Example_SLURM_scripts#granular-resource-allocation-with-srun) for example.
- `--mem=4g`: amount of memory requested (4 gigabytes)
- `--pty`: executes task in pseudo terminal mode
- `-J myInteractiveJob`: name of the job (optional)
- `/bin/bash`: the program to run, in this case `bash`

After running the command, observe the output to see if what you requested is actually allocated (under `defined options`). Notice the last line `srun: Node arctrdcn001, 1 tasks started`, which means the task started successfully on a compute node `arctrdcn001.rs.gsu.edu`, hence the prompt has changed to `campusID@arctrdcn001`. Otherwise if there is an error, observe the output for possible reasons.

Check out [Running GUI applications](Running_GUI_applications) to see how to run GUI applications on the cluster.

`srun` command has many options available to control what resource are allocated and how tasks are distributed across those resources: https://slurm.schedmd.com/srun.html