---
layout: default
title: Cluster do's & don'ts
nav_order: 9
parent: Getting Started
---
### Do limit the number of simultaneously running tasks

If you want to run `N` tasks but not use the whole cluster and leave
some resources for others to use, you can use
`sbatch --array=1-N%m `<job submission script> to limit the number of
simultaneously running jobs to `m`. There are currently 544 cores in the
qTRD partition, so do limit the number of tasks to at most half of it
and leave resources free for the others.

### Don't run any CPU/memory intensive task on the login node

The login node is used by *all* the users in TReNDS for submitting jobs,
starting interactive sessions and hopping on to the DEV nodes. As a
result, any CPU/memory intensive task (such as running a computation in
Matlab for hours) disrupts all of these processes and slows *everyone*
down.

### Don't run any lengthy CPU/memory intensive task on the DEV nodes

The dev node is used by *many* users in TReNDS for tweaking and
debugging codes, examining data, running services that support research
etc. As a result, any CPU/memory intensive task (such as running a
computation in Matlab for hours) disrupts all of these processes and
slows the other users down.

### Don't ssh directly on to one of the compute nodes and run analysis

The SLURM job scheduler allocates resources based on the requested
CPU/memory of all users. If someone bypasses the scheduler and runs
analysis (including Jupyter notebooks) on the worker nodes, it may
exhaust resources and cause unpredictable issues. So far we have seen
jobs terminating without any error, jobs terminating with segmentation
faults and out-of-memory errors, corrupted files being written to the
disk, very slow response to any kind of command etc.

### Do limit number of threads

Jobs should only have access to the number of CPUs actually
requested. But still take care to specify the number of parallel threads in our code less than or equal to the allocation.

Note that SLURM is not meant to *limit* resources, but is the way to
communicate what resource you need/use to the other users.

### Don’t run suboptimal scripts on the cluster

It may exhaust resources and cause unpredictable issues. Use the
interactive mode instead or ask for help with optimization.