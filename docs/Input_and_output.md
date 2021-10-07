---
layout: default
title: Input and output
nav_order: 3
parent: SLURM Overview
---
### SLURM output and error files

SLURM job output and errors are written out to `out%A.out` and
`error%A.err` files respectively, with `%A` being replaced by the job
ID. The files are written respective to the directory where the job is
submitted from, unless absolute path is specified in the `SBATCH`
directive.

```
#SBATCH -e error%A.err
#SBATCH -o out%A.out
```

In case of a job array, `%a` is replaced with the array ID.

```
#SBATCH -e error%A-%a.err
#SBATCH -o out%A-%a.out
```

### `/runjobs`

For fast file I/O performance, it is advisable to use the `/runjobs`
volume attached to the nodes.