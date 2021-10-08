---
layout: default
title: GPU Computing
nav_order: 2
parent: List of software
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## GPU queue/partitions

| Partitions                                    | Nodes                                           | Time limit | Priority | CPUs  | Memory     | GPUs                | Limitations         | Preemption |
|-----------------------------------------------|-------------------------------------------------|------------|----------|-------|------------|---------------------|---------------------|------------|
| qTRDGPUH                                      | trendsdgx001.rs.gsu.edu-trendsdgx004.rs.gsu.edu | 5d 8h      | high     | 40    | 512GB      | gpu:v100:8          | Max 4 GPUs per user | N/A        |
| trendsgn001.rs.gsu.edu-trendsgn002.rs.gsu.edu | 5d 8h                                           | high       | 40       | 192GB | gpu:v100:4 | Max 4 GPUs per user | N/A                 |            |
| qTRDGPUM                                      | trendsdgx001.rs.gsu.edu-trendsdgx004.rs.gsu.edu | 5d 8h      | medium   | 40    | 512GB      | gpu:v100:8          | Max 8 GPUs per user | suspend    |
| trendsgn001.rs.gsu.edu-trendsgn002.rs.gsu.edu | 5d 8h                                           | medium     | 40       | 192GB | gpu:v100:4 | Max 8 GPUs per user | suspend             |            |
| qTRDGPUL                                      | trendsdgx001.rs.gsu.edu-trendsdgx004.rs.gsu.edu | 5d 8h      | low      | 40    | 512GB      | gpu:v100:8          | N/A                 | suspend    |
| trendsgn001.rs.gsu.edu-trendsgn002.rs.gsu.edu | 5d 8h                                           | low        | 40       | 192GB | gpu:v100:4 | N/A                 | suspend             |            |
| qTRDGPU                                       | trendsagn001.rs.gsu.edu-trendsagn020.rs.gsu.edu | 5d 8h      | N/A      | 64    | 512GB      | gpu:gforce:1        | N/A                 | N/A        |

## Special nodes

| Nodes                     | CPUs | Memory | GPUs         | Purpose                   |
|---------------------------|------|--------|--------------|---------------------------|
| trendsgndev101.rs.gsu.edu | 4    | 62GB   | TITAN X:2    | GPU development & testing |
| trendsagn019.rs.gsu.edu   | 64   | 512GB  | gpu:gforce:1 | GPU development & testing |

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
#SBATCH -A PSYC0002
#SBATCH --oversubscribe
#SBATCH --mail-type=ALL
#SBATCH --mail-user=<email address>

sleep 5s

export OMP_NUM_THREADS=1
export MODULEPATH=/apps/Compilers/modules-3.2.10/Debug-Build/Modules/3.2.10/modulefiles/
echo $HOSTNAME >&2

source <path to conda installation>/bin/activate <name/path of conda environment>

python script.py --arg1 $SLURM_ARRAY_TASK_ID &
python script.py --arg1 $SLURM_ARRAY_TASK_ID &
wait

sleep 10s
```

### Submitting the job

`sbatch --array=1-8%2 JobSubmit.sh`

## Start interactive mode/terminal/bash on GPU worker/compute nodes

*can be run on the login node*
```
# Start interactive mode on a GPU worker node
$ srun -p qTRDGPUH -A PSYC0002 -v -n1 --pty --mem=10g --gres=gpu:v100:1 /bin/bash
```