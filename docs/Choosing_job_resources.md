---
layout: default
title: Choosing job resources
nav_order: 2
parent: SLURM Overview
---
Suppose we start an interactive session like so:

`$ srun -p qTRD -A PSYC0002 -v -n1 --mem=10g -t60 --pty --x11 /bin/bash`

Above in the `srun` command we have specified `--mem=10g`, which means
we have allocated 10 GigaBytes (GB) of memory (and 1 CPU by default) for
our work. If the estimated memory required by your work is higher than
10GB, you have to start a new session with the proper amount of RAM.
Things to consider:

-   If the required memory is about 10-100GB, it is usually OK start a
    session with `--mem=100g`. By default, the task is allocated to one
    CPU in one of the general compute nodes (which have 32 CPUs and 768
    GB of memory each).

<!-- -->

-   If the required memory is about 100-600GB, consider allocating
    multiple corresponding CPUs in addition to memory. Otherwise, up to
    31 tasks could be allocated to the same node and it may run out of
    memory.

`>> maxNumCompThreads(10);`

-   On the other hand, if using parallel pool, first increase the amount
    of resource available using the following command in the Linux
    command line or `sbatch` script (to avoid segmentation faults):

`ulimit -u 63536`

Then start Matlab, then start
parallel pool in the command window or script with the number of CPUs
allocated.

```
# tell Matlab to run 10 parallel processes in the command window or your script
>> parpool(10);
```

-   If the required memory *for a single task* is over 700GB, consider
    using the high-memory nodes/queue. But you still must allocate CPUs
    and memory properly, like so:

```
# allocate 80 CPUs and 1TB of memory in the high memory queue in SLURM
$ srun -p qTRDHM -A PSYC0002 -v -n1 -c80 --mem=1t --pty --x11 /bin/bash 
$ module load Framework/Matlab2019b
$ matlab &
```

And then specify the proper number of threads/parallel processes.

### Estimating memory requirement

-   It depends on your job.
-   It is important to understand how your program handles memory in
    order to optimize and reduce excess memory/resource usage and
    improve performance on the cluster.
-   It is also important to understand how your program stores data.
-   If the memory requirements are high, you are better off splitting it
    across multiple nodes using SLURM job arrays.

GIFT gives an estimate of memory usage when running a Group ICA
analysis. Tips for optimizing Matlab programs can be found
[here](https://www.mathworks.com/help/matlab/matlab_prog/strategies-for-efficient-use-of-memory.html)
and
[here](https://www.mathworks.com/help/matlab/performance-and-memory.html?s_tid=CRUX_lftnav).