---
layout: default
title: Example SLURM scripts
nav_order: 5
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

## For submitting jobs to the cluster

### Sample SBATCH (`JobSubmit.sh`) script
[https://slurm.schedmd.com/sbatch.html](https://slurm.schedmd.com/sbatch.html)

```
#!/bin/bash
#SBATCH -N 1
#SBATCH -n 1
#SBATCH -c 1
#SBATCH --mem=10g
#SBATCH -p qTRD
#SBATCH -t 1440
#SBATCH -J <job name>
#SBATCH -e error%A.err
#SBATCH -o out%A.out
#SBATCH -A <slurm_account_code>
#SBATCH --mail-type=ALL
#SBATCH --mail-user=<email address>
#SBATCH --oversubscribe

sleep 10s

echo $HOSTNAME >&2

module load matlab/R2022a
matlab -batch 'simple_example'

sleep 10s
```

Same script with annotations:

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
#SBATCH -A <slurm_account_code>     # user group. See "requesting an account" page for list of groups
#SBATCH --mail-type=ALL # types of emails to send out. See SLURM documentation for more possible values
#SBATCH --mail-user=<email address> # set this email address to receive updates about the job
#SBATCH --oversubscribe # see SLURM documentation for explanation

# it is a good practice to add small delay at the beginning and end of the job- helps to preserve stability of SLURM controller when large number of jobs fail simultaneously 
sleep 10s

# for debugging purpose- in case the job fails, you know where to look for possible cause
echo $HOSTNAME >&2

# run the actual job
module load matlab/R2022a
matlab -batch 'simple_example'

# delay at the end (good practice)
sleep 10s
```

-   The above will allocate 1 CPU, 10GB RAM on one of the nodes in the
    `qTRD` queue for 1 day (1440 minutes) or as long as the job runs,
    whichever is shorter.
-   `<slurm_account_code>` indicates the job account, or which project the submitter
    belongs to.
-   The job output and errors will be written out to `out%A.out` and
    `error%A.err` files respectively, with `%A` being replaced by the
    job ID.
-   Job status (start/complete/failed etc.) will be emailed out as well.

### Submitting the job

`$ sbatch JobSubmit.sh`

## Creating job arrays

### Sample SBATCH (`JobSubmit.sh`) script
[https://slurm.schedmd.com/job_array.html](https://slurm.schedmd.com/job_array.html)

```
#!/bin/bash
#SBATCH -N 1
#SBATCH -n 1
#SBATCH -c 1
#SBATCH --mem=10g
#SBATCH -p qTRD
#SBATCH -t 1440
#SBATCH -J <job name>
#SBATCH -e error%A-%a.err
#SBATCH -o out%A-%a.out
#SBATCH -A <slurm_account_code>
#SBATCH --mail-type=ALL
#SBATCH --mail-user=<email address>
#SBATCH –oversubscribe

sleep 10s

echo $HOSTNAME >&2

module load matlab/R2022a
matlab -batch 'array_example($SLURM_ARRAY_TASK_ID)'

sleep 10s
```

### Submitting the job

`$ sbatch --array=1-8%2 JobSubmit.sh`

The above will execute the same job 8 times, each time with a different
`SLURM_ARRAY_TASK_ID` environment variable value ranging between 1-8. 2
jobs will be run simultaneously.

### Running more jobs than the array size limit 
The cluster has a limit of 5000 on the array size, meaning you cannot schedule more than 5000 job steps in an array. If you have more than 5000 tasks to run, you can run a smaller loop inside each job step. Following is an example in Matlab:

```
things_ = 5000;
total_ = 44000;

start_ = str2num( getenv('SLURM_ARRAY_TASK_ID') );
for ii = start_:things_:total_
    do_thing(ii);
end

function do_thing( num )
    disp(num)
end
```

Following is an example in bash:

```
#!/bin/bash

THINGS=5000
TOTAL=44000

START=$SLURM_ARRAY_TASK_ID
for ii in $(seq $START $THINGS $TOTAL)
do
    echo $ii
done
```

Submit the job using `sbatch --array=1-5000%100 JobSubmit.sh`.

## Job array with multiple tasks on each GPU

### The `JobSubmit.sh` file

```
#!/bin/bash
#SBATCH -N 1
#SBATCH -n 1
#SBATCH -c 10
#SBATCH --mem=50g
#SBATCH --gres=gpu:v100:1
#SBATCH -p qTRDGPUH
#SBATCH -t 4-00
#SBATCH -J <job name>
#SBATCH -e error%A-%a.err
#SBATCH -o out%A-%a.out
#SBATCH -A <slurm_account_code>
#SBATCH --oversubscribe
#SBATCH --mail-type=ALL
#SBATCH --mail-user=<email address>

sleep 10s

echo $HOSTNAME >&2

source <path to conda installation>/bin/activate <name/path of conda environment>

python script.py --arg1 $SLURM_ARRAY_TASK_ID &
python script.py --arg1 $SLURM_ARRAY_TASK_ID &
wait

sleep 10s
```

### Submitting the job

`$ sbatch --array=1-8%2 JobSubmit.sh`

## Granular resource allocation with `srun`

See SLURM documentation for details:
<https://slurm.schedmd.com/srun.html#lbAN>

The following `sbatch` script allocates 2 nodes for a job. Then it uses
the `srun` command to execute two different Matlab scripts on each node.

```
#!/bin/bash
#SBATCH -N 2
#SBATCH -n 2
#SBATCH -c 10
#SBATCH --mem=100g
#SBATCH -p qTRD
#SBATCH -t 1440
#SBATCH -J <campusID>
#SBATCH -e error%A.err
#SBATCH -o out%A.out
#SBATCH -A <slurm_account_code>
#SBATCH --oversubscribe

sleep 10s

echo $HOSTNAME >&2 

module load matlab/R2022a
srun -N1 -n1 numactl --localalloc matlab -batch 'script1' &
srun -N1 -n1 numactl --localalloc matlab -batch 'script2' &

wait

sleep 10s
```
