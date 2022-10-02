---
layout: default
title: Input and output
nav_order: 3
parent: SLURM Overview
last_modified_date: 10/2/2022 16:38
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

### SLURM output and error files

SLURM job output and errors are written out to `out%A.out` and
`error%A.err` files respectively, with `%A` being replaced by the job
ID. The files are written respective to the directory where the job is
submitted from, unless absolute path is specified in the `SBATCH`
directive. Add the following in the `sbatch` job submission script: 

```
#SBATCH -e error%A.err
#SBATCH -o out%A.out
```

In case of a job array, use the following format so that `%a` is replaced with the job step#.

```
#SBATCH -e error%A-%a.err
#SBATCH -o out%A-%a.out
```

### `/scratch`

For fast file I/O performance, it is advisable to use the `/scratch` volume attached to the nodes.

```
# copying test_python.py from projects directory to /scratch directory
cp <your project directory>/test_python.py $SCRATCH

module load Python
python test_python.py

# copying output (results.txt) to the project directory
cp results.txt <your project directory>
rm -rf $SCRATCH
```
