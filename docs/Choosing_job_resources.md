---
layout: default
title: Choosing job resources
nav_order: 2
parent: SLURM Overview
last_modified_date: 10/2/2022 16:03
---
Suppose we start an interactive session like so:

`$ srun -p qTRD -A <slurm_account_code> -v -n1 --mem=10g -t60 --pty /bin/bash`

Above in the `srun` command we have specified `--mem=10g`, which means
we have allocated 10 GigaBytes (GB) of memory (and 1 CPU by default) for
our work. If the estimated memory required by your work is higher than
10GB, you have to start a new session with the proper amount of RAM.
Things to consider:

-   If the required memory is about 10-100GB, it is usually OK start a
    session with `--mem=100g`. By default, the task is allocated to one
    CPU in one of the general compute nodes (which have 32 CPUs and 768
    GB of memory each).

-   If the required memory is about 100-600GB, consider allocating
    multiple corresponding CPUs in addition to memory. Otherwise, up to
    31 tasks could be allocated to the same node and it may run out of
    memory. The following will allocate 10 CPUs.

`$ srun -p qTRD -A <slurm_account_code> -v -n1 -c10 --mem=100g -t60 --pty /bin/bash`

-   On the other hand, if using parallel pool, run the following in command window or script and specify the number number of parallel processes equal to the number of CPUs allocated.

```
# tell Matlab to run 10 parallel processes in the command window or your script
>> parpool(10);
```

-   If the required memory *for a single task* is over 700GB, consider
    using the high-memory nodes/queue. But you still must allocate CPUs
    and memory properly, like so:

```
# allocate 80 CPUs and 1TB of memory in the high memory queue in SLURM
$ srun -p qTRDHM -A <slurm_account_code> -v -n1 -c80 --mem=1t --pty /bin/bash 
$ module load matlab/R2022a
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