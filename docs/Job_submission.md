---
layout: default
title: Job Submission Overview
nav_order: 1
parent: SLURM Overview
---
## Job submission overview

## Controlling jobs

The following commands can be run on the login node:

```
# Check status of all jobs
$ squeue

# Check status of jobs by user
$ squeue -u `<campusID>

# Continuously check status of jobs
$ watch -n 10 squeue -u `<campusID>

# Check job status by ID
$ squeue -j `<jobID>

# Cancel job by ID
$ scancel `<jobID>
```

## SBATCH scripting guide

## Multiple jobs with job arrays

## Sample SBATCH scripts

Please see [Example_SLURM_scripts](Example_SLURM_scripts)