---
layout: default
title: Cluster do's & don'ts
nav_order: 9
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

### Do limit the number of simultaneously running tasks

If you want to run `N` tasks but not use the whole cluster and leave
some resources for others to use, you can use
`sbatch --array=1-N%m `<job submission script> to limit the number of
simultaneously running jobs to `m`. There are currently 544 cores in the
qTRD partition, so do limit the number of tasks to at most half of it
and leave resources free for the others.

### Do NOT run any non-SLURM task on the login node

The login node is used by *all* the users in TReNDS for submitting jobs,
starting interactive sessions and hopping on to the DEV nodes. As a
result, any CPU/memory intensive task (such as running a computation in
Matlab for hours) disrupts all of these processes and slows *everyone*
down. *This includes VSCode - VSCode runs a server on the node that eats up
CPU and RAM resources and can create issues when left unchecked. If using
VSCode, connect to a dev node directly*. 

### Do NOT run any lengthy CPU/memory intensive task on the DEV nodes

The dev node is used by *many* users in TReNDS for tweaking and
debugging codes, examining data, running services that support research
etc. As a result, any CPU/memory intensive task (such as running a
computation in Matlab for hours) disrupts all of these processes and
slows the other users down.

### Do allocate Compute Resources Fairly

There is no perfect guide to picking the optimal selection of numbers of CPU, amount of RAM, and other resources for 
general tasks in neuroimaging analysis; however, we ask that you use common sense and consider some rules of thumb when allocating resources.
In general, think about how the resources you are using might block others from using the remaining resources on a node. 
For example, if a node in qTRD has 32 CPUs and 768 GB of RAM, and you request all 32 CPUs but only 500 GB of RAM, there will be 268 GB of RAM that 
go unused and are inaccessible to other users. 

One suggested rule of thumb for CPU-only machines is to divide the amount of RAM by the number of CPUs, say 768/32 = 24 GB/CPU. Then, when selecting your # of CPUs and RAM, check that the ratio of RAM to CPU roughly aligns with this number. So if I request 4 CPUs, I should try to use about 96 GB of RAM for example. These recommendations are not hard and fast; however, they give you a decent benchmark to check that you are allocating resources fairly. 
For GPU machines, typically dividing the amount of RAM and number of CPUs by the number of GPUs on the machine will give you a good estimate of per-GPU resources that can be fairly allocated. 

### Do NOT ssh directly on to one of the compute nodes and run analysis

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

### Do NOT copy data

Unless specifically requested by your PI, if data lives permanently in a shared folder or somewhere where you can access it directly, 
do not copy raw data, phenotype information, or other data set materials into your personal folders. In addition to using up extra space, 
this can create compliance issues when Data Usage Agreements expire or change storage regulations. 

### Do NOT run suboptimal scripts on the cluster

It may exhaust resources and cause unpredictable issues. Use the
interactive mode instead or ask for help with optimization.

### Do Communicate when IT and Cluster Admins Reach Out

TReNDs faculty and staff (e.g. Dr. Baker or Dr. Plis) or GSU IT may reach out regarding your usage on the cluster via slack or email. When TReNDs faculty and staff reach out, 

### Do use common sense and obey the law/ GSU Policy

It hopefully goes without saying, but use common sense when utilizing the shared resources. Do not use the cluster for any illegal purposes or for activities which violate [GSU policy](https://technology.gsu.edu/technology-services/cybersecurity/university-technology-policies/) 
