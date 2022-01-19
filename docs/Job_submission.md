---
layout: default
title: Job Submission Overview
nav_order: 1
parent: SLURM Overview
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Job submission overview

You can use SLURM in different ways to submit jobs:

- Interactive mode: [see here for an example](SLURM_overview#srun-create-a-resource-allocation-and-launch-the-tasks-for-a-job-step).
- GUI applications: [see here for an example](Running_GUI_applications#run-the-application)
- `sbatch` scripts: [see below for an example](Job_submission#sbatch-scripting-guide).

## SBATCH scripting guide

See the following example with annotations. 

```
#!/bin/bash
#SBATCH -N 1            # number of requested nodes. Set to 1 unless needed.  
#SBATCH -n 1            # number of tasks to run. Set to 1 unless needed. See granular resource allocation below for example.
#SBATCH -c 1            # number of requested CPUs
#SBATCH --mem=10g       # amount of memory requested (g=gigabytes)
#SBATCH -p qTRD         # partition to run job on. See "cluster and queue information" page for more information.
#SBATCH -t 1440         # time in minutes. After set time the job will be cancelled. See "cluster and queue information" page for limits.
#SBATCH -J <job name>
#SBATCH -e error%A.err  # errors will be written to this file. If saving this file in a separate folder, make sure the folder exists, or the job will fail
#SBATCH -o out%A.out    # output will be written to this file. If saving this file in a separate folder, make sure the folder exists, or the job will fail
#SBATCH -A PSYC0002     # user group. See "requesting an account" page for list of groups
#SBATCH --mail-type=ALL # types of emails to send out. See SLURM documentation for more possible values
#SBATCH --mail-user=<email address> # set this email address to receive updates about the job
#SBATCH --oversubscribe # see SLURM documentation for explanation

# it is a good practice to add small delay at the beginning and end of the job- helps to preserve stability of SLURM controller when large number of jobs fail simultaneously 
sleep 10s

# number of threads for certain C libraries. Leave it like this unless necessary
export OMP_NUM_THREADS=1
# location of module files. In case the allocated node fails to initiate properly, this is help load the modules and run the job
export MODULEPATH=/apps/Compilers/modules-3.2.10/Debug-Build/Modules/3.2.10/modulefiles/
# for debugging purpose- in case the job fails, you know where to look for possible cause
echo $HOSTNAME >&2

# run the actual job
module load Framework/Matlab2019b
echo matlab -batch 'simple_example'

# delay at the end (good practice)
sleep 30s
```

Save the above script in your `/data/user*/<your name>` directory as `JobSubmit.sh` and modify as needed. Then submit the job using the following command:

`$ sbatch JobSubmit.sh`

Then use the commands in the following controlling jobs section to keep tabs on the job.

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

## Multiple jobs with job arrays

You can submit a number of identical jobs (e.g. fMRI preprocessing) using the SLURM job array feature (https://slurm.schedmd.com/job_array.html).
The number or maximum jobs that can be submitted is 5000. 
Please see [this example](Example_SLURM_scripts#running-more-jobs-than-the-array-size-limit) if you need to submit more than that.

### Submitting job arrays

```
# submit 100 jobs, run 10 at a time. Please use a sensible limit and leave resources for the others.
$ sbatch --array=1-100%10 JobSubmit.sh

# submit 100 jobs without limitation
$ sbatch --array=1-100 JobSubmit.sh

# run particular tasks 
$ sbatch --array=2,4,8,16,32,65  JobSubmit.sh
```

### Modifying job arrays

Running the following command will update the task limit (e.g. `%10` in the above section) of a running array.

```
$ scontrol update ArrayTaskThrottle=<count> JobId=<jobID>
```

### Input and output files

You can add/edit the following in the job submission script so that `%A` and `%a` will be replaced by the job ID and the array task ID, respectively. 

```
#SBATCH --output=out%A_%a.out
#SBATCH --error=error%A_%a.err
```

### The array ID index

SLURM provides an environment variable `$SLURM_ARRAY_TASK_ID` which you can reference inside your script to control input and output. Following are some examples (adapted from [here](https://help.rc.ufl.edu/doc/SLURM_Job_Arrays#Using_the_array_ID_Index)):

```
# read a particular input file in a folder containing *.txt files 
$ file=$(ls *.txt | sed -n ${SLURM_ARRAY_TASK_ID}p)
$ myscript -i $file

# read a particular line from an input file containing a list of IDs
ID_LIST=($(<input.csv))
ID=${ID_LIST[${SLURM_ARRAY_TASK_ID}]}

# use array ID in a python script
> import sys
> task_id = sys.getenv('SLURM_ARRAY_TASK_ID') 

# use array ID in a Matlab script
> task_id = getenv('SLURM_ARRAY_TASK_ID') 

# use array ID in an R script
> task_id <- Sys.getenv("SLURM_ARRAY_TASK_ID")
```

## Sample SBATCH scripts

Please see [Example SLURM scripts](Example_SLURM_scripts)