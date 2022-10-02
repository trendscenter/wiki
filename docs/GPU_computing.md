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

| Partitions     | GPUs                | Nodes         | CPUs  | Memory     | Time limit | 
|----------------|---------------------|---------------|------------|-------|------------|
| qTRDGPU[H/M/L] | gpu:V100:8          | dgx001-dgx004 | 40    | 512GB      | 5d 8h      |
|                | gpu:V100:4          | gn001-gn002   | 40    | 192GB      | 5d 8h      |
|                | gpu:a100:8          | dgxa001       | 40    | 1TB        | 5d 8h      |
| qTRDGPU        | gpu:gforce:1        | agn001-agn020 | 64    | 512GB      | 5d 8h      |

## GPU partitions preemption rule 

| Partitions     | Priority | Limitations         | Preemption |
|----------------|----------|---------------------|------------|
| qTRDGPUH       | high     | Max 4 GPUs per user | N/A        |
| qTRDGPUM       | medium   | Max 8 GPUs per user | suspend    |
| qTRDGPUL       | low      | N/A                 | suspend    |
| qTRDGPU        | N/A      | N/A                 | N/A        |

## Special nodes

| Nodes                     | CPUs | Memory | GPUs         | Purpose                   |
|---------------------------|------|--------|--------------|---------------------------|
| trendsgndev101.rs.gsu.edu | 4    | 62GB   | TITAN X:2    | GPU development & testing |
| trendsagn019.rs.gsu.edu   | 64   | 512GB  | gpu:gforce:1 | GPU development & testing |

## Allocating GPUs in SLURM

When allocating GPUs in SLURM, use the value in the GPUs column in the above table as the `--gres` parameter.
See examples below.

## Job array with multiple tasks on each GPU

### The `JobSubmit.sh` file

```
#!/bin/bash
#SBATCH -N 1
#SBATCH -n 1
#SBATCH -c 10
#SBATCH --mem=50g
#SBATCH --gres=gpu:V100:1
#SBATCH -p qTRDGPUH
#SBATCH -t 4-00
#SBATCH -J <job name>
#SBATCH -e error%A-%a.err
#SBATCH -o out%A-%a.out
#SBATCH -A <slurm_account_code>
#SBATCH --oversubscribe
#SBATCH --mail-type=ALL
#SBATCH --mail-user=<email address>

sleep 5s

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
$ srun -p qTRDGPUH -A <slurm_account_code> -v -n1 --pty --mem=10g --gres=gpu:V100:1 /bin/bash
```