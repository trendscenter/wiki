---
layout: default
title: FAQ
nav_order: 7
---
## Common cluster errors and remedies

### matlab: command not found

-   Load the Matlab module

`$ module load Framework/Matlab2019b`

-   Set the `MODULEPATH` variable

`$  export MODULEPATH=/apps/Compilers/modules-3.2.10/Debug-Build/Modules/3.2.10/modulefiles/`

### Error using parpool ... Parallel pool failed to start with the following error ...

-   Delete contents of `~/.matlab/local_cluster_jobs`

`$ rm -r ~/.matlab/local_cluster_jobs`

-   Delete contents of `~/.matlab`

`$ rm -r ~/.matlab`

### No space left on device

-   The storage system you are trying to use is full. Try to identify
    the particular storage system and delete some unneeded files from
    there.

### No such file or directory

-   The path you specified is not accessible from the node where the job
    is running. Identify the node by putting `echo $HOSTNAME` at the
    beginning of your `sbatch` script. Try to start an interactive
    session on the said node and see if the directory is accessible from
    the command line.

### Job does not run and there is no \*.out or \*.err file

-   Make sure the directory where the out/err files are supposed to be
    written exists.
-   It is possible that the node where the job step was scheduled has
    dropped storage mount. Try to identify the node where the job was
    scheduled using either one of the following commands:

`$ squeue -j `<jobID>
`$ sacct -j `<jobID>` --format=jobid,elapsed,ncpus,ntasks,state,NodeList`

### setfacl: permission not supported

-   It might be an NFS4 volume, use `nfs4_setfacl` instead: [Permissions
    on NFS volumes](Storage_guide#Permissions_on_NFS_volumes)

## Other questions

### How can I get information about CPU/memory of the cluster

`$ sinfo -o "%24n %7P %.11T %.4c %.8m %14C %10e"`
`HOSTNAMES                PARTITI       STATE CPUS   MEMORY CPUS(A/I/O/T)  FREE_MEM`
`trendscn001.rs.gsu.edu   qTRD          mixed   32   768697 2/30/0/32      716707`
`trendscn004.rs.gsu.edu   qTRD          mixed   32   768697 15/17/0/32     409574`
`trendscn007.rs.gsu.edu   qTRD          mixed   32   768697 16/16/0/32     653037`
`trendscn008.rs.gsu.edu   qTRD          mixed   32   768697 1/31/0/32      562276`
`trendscn011.rs.gsu.edu   qTRD          mixed   32   768697 16/16/0/32     461971`
`trendscn016.rs.gsu.edu   qTRD          mixed   32   768697 16/16/0/32     275150`
`trendscn009.rs.gsu.edu   qTRD      allocated   32   768697 32/0/0/32      484949`
`trendscn010.rs.gsu.edu   qTRD      allocated   32   768697 32/0/0/32      436889`
`trendscn012.rs.gsu.edu   qTRD      allocated   32   768697 32/0/0/32      407470`
`trendscn002.rs.gsu.edu   qTRD           idle   32   768697 0/32/0/32      691967`
`trendscn003.rs.gsu.edu   qTRD           idle   32   768697 0/32/0/32      535892`
`trendscn005.rs.gsu.edu   qTRD           idle   32   768697 0/32/0/32      629969`
`trendscn006.rs.gsu.edu   qTRD           idle   32   768697 0/32/0/32      661117`
`trendscn013.rs.gsu.edu   qTRD           idle   32   768697 0/32/0/32      702867`
`trendscn014.rs.gsu.edu   qTRD           idle   32   768697 0/32/0/32      625527`
`trendscn015.rs.gsu.edu   qTRD           idle   32   768697 0/32/0/32      708471`
`trendscn019.rs.gsu.edu   qTRDEV         idle   32   769700 0/32/0/32      514230`
`trendscn020.rs.gsu.edu   qTRDEV         idle   32   769700 0/32/0/32      710871`
`trendsmn001.rs.gsu.edu   qTRDHM        mixed   96  1541404 22/74/0/96     971640`
`trendsmn002.rs.gsu.edu   qTRDHM        mixed   96  1541404 15/81/0/96     1122162`
`trendsmn003.rs.gsu.edu   qTRDHM         idle   96  1541404 0/96/0/96      1296288`
`trendsgn001.rs.gsu.edu   qTRDGPU       mixed   40   190669 30/10/0/40     9514`
`trendsgn002.rs.gsu.edu   qTRDGPU   allocated   40   190669 40/0/0/40      1287`
`trendsgn001.rs.gsu.edu   qTRDGPU       mixed   40   190669 30/10/0/40     9514`
`trendsgn002.rs.gsu.edu   qTRDGPU   allocated   40   190669 40/0/0/40      1287`

Above example shows the nodes, which partition each of them belongs to,
their state (state of the CPUs, idle/allocated/mixed), total CPUSs and
memory, number of CPUs allocated/idle/other/total (A/I/O/T), and free
memory.

On a general purpose compute or high memory node, you can get
information (configuration and usage) about the CPUs by running `htop`
command. On a GPU node, you can get information about the GPUs by
running `nvidia-smi` command.

### How do I allocate/avoid allocating a particular node?

Using a command-separated list of hostnames in the `--nodelist` or
`-exclude` argument of `srun/sbatch`.

### How can I limit the number of simultaneously running tasks?

If you want to run `N` tasks but not use the whole cluster and leave
some resources for others to use, you can use
`sbatch --array=1-N%m `<job submission script> to limit the number of
simultaneously running jobs to `m`.

### What is the max time-limit for jobs?

Currently 5 days and 8 hours. Use `sinfo` command to view time limit for
different queues.

### How can I increase time-limit of running jobs?

The following command does it:

`$ scontrol update jobid=`<job_id>` TimeLimit=`<new_timelimit>

### How can I update task limit of a running job array?

The following command does it:

`$ scontrol update ArrayTaskThrottle=`<count>` JobId=`<jobID>

### Who are the users with administrative privilege?

Vince <vcalhoun>, Sergey <splis>, Suranga <neranjan>.

### Why should I not run any CPU/memory intensive task on the login node?

The login node is used by *all* the users in TReNDS for submitting jobs,
starting interactive sessions and hopping on to the DEV nodes. As a
result, any CPU/memory intensive task (such as running a computation in
Matlab for hours) disrupts all of these processes and slows *everyone*
down.

### Why should I not ssh directly on to one of the compute nodes and run my analysis?

The SLURM job scheduler allocates resources based on the requested
CPU/memory of all users. If someone bypasses the scheduler and run
analysis on the worker nodes, it may exhaust resources and cause
unpredictable issues.

### What kind of unpredictable issues can be caused?

So far we have seen jobs terminating without any error, jobs terminating
with segmentation faults and out-of-memory errors, corrupted files being
written to the disk, very slow response to any kind of command etc.

### Why am I getting "error: Unable to allocate resources: Invalid account or account/partition combination specified"

You may have specified invalid project code. Please take a note of the
following project codes:

`Dr. Vince Calhoun's group   PSYC0002`
`BrainForge group            PSYC0003`
`Dr. Jessica Turner's group  PSYC0004`
`Dr. Jingyu Liu's group      PSYC0005`

### My job completed without any error, but there is nothing in the output!

Did you write the job submission script in a Windows system, then
transferred it to the cluster? You may need to convert the line-endings
in that file using `dos2unix `<filename> command.

### Why does my job not start?

Use `squeue -u `<campusID> to check the state and reason. To find what
the state means, [see
this](https://slurm.schedmd.com/squeue.html#SECTION_JOB-STATE-CODES). To
find what the reason means, [see
this](https://slurm.schedmd.com/squeue.html#SECTION_JOB-REASON-CODES).
Some common states:

CG COMPLETING
Job is in the process of completing. Some processes on some nodes may
still be active.

F FAILED
Job terminated with non-zero exit code or other failure condition.

OOM OUT_OF_MEMORY
Job experienced out of memory error.

PD PENDING
Job is awaiting resource allocation.

PR PREEMPTED
Job terminated due to preemption.

R RUNNING
Job currently has an allocation.

S SUSPENDED
Job has an allocation, but execution has been suspended and CPUs have
been released for other jobs.

### Why is my job in PD (pending) state?

SLURM uses fair tree algorithm to decide the priority of pending jobs.
Once resource is available, the pending job with highest priority is
immediately allocated. To view the priority, use `sprio -l` command. To
learn more about the fair tree algorithm, [see
this](https://slurm.schedmd.com/fair_tree.html).

### Starting Matlab parallel pool is causing segmentation fault...

Try the following command before starting Matlab-

`ulimit -u 63536`

You can also add the command to your .bashrc and sbatch scripts. The
command makes the maximum number of processes available to a single
user.

### Can I download this wiki?

There is a "printable version" link on the sidebar on every page. You
can also add `?printable=yes` of a page URL and save a printable
version; or directly print a page.

### I am getting "X Error of failed request: BadValue" error in XQuartz

Try running the following command in the terminal to fix issues with
some GUI applications: (Thanks to Leyla Eghbalzad for figuring this out)

`defaults write org.macosforge.xquartz.X11 enable_iglx -bool true`

Or, you may have to try downgrading to Xquartz version 2.7.8 [per this
thread](https://bugs.freedesktop.org/show_bug.cgi?id=96433).