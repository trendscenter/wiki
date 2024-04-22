---
layout: default
title: Cluster & queue information
nav_order: 7
parent: Getting Started
last_modified_date: 09/25/2022 11:18
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Cluster configuration

| Number | Manufacturer | Cores | RAM    | GPUs          | GPU Memory | Name                |
| ------ | ------------ | ----- | ------ | ------------- | ---------- | ------------------- |
| 20     | Intel        | 32    | 768 GB |               |            | arctrdcn{001-020}   |
| 3      | Intel        | 96    | 1.5 TB |               |            | arctrdhm{001-003}   |
| 20     | AMD          | 64    | 512 GB | 1xNvidia 2080 | 11GB       | arctrdagn{001-020}  |
| 16     | AMD          | 128   | 512 GB | 2xNvidia A40  | 45GB       | arctrdagn{031-046}  |
| 1      | Nvidia DGX-1 | 256   | 1 TB   | 8xNvidia A100 | 40GB       | arctrddgxa001       |
| 2      | Nvidia DGX-1 | 192   | 1 TB   | 8xNvidia A100 | 80GB       | arctrddgxa{002-003} |
| 2      | Dell         | 40    | 192 GB | 4xNvidia V100 | 32GB       | arctrdgn{001-002}   |

## CPU queue/partitions

| Partitions | Nodes                      | Time limit | Priority | CPUs | Memory | GPUs    | Limitations | Preemption | Purpose                                                          |
| ---------- | -------------------------- | ---------- | -------- | ---- | ------ | ------- | ----------- | ---------- | ---------------------------------------------------------------- |
| qTRD       | arctrdcn001-arctrdcn016    | 5d 8h      | N/A      | 32   | 768GB  | N/A     | N/A         | N/A        | General purpose (production) computing                           |
| qTRDGPU    | arctrdagn[001-020,031-046] | 5d 8h      | N/A      | 64   | 512GB  | gpu:RTX | N/A         | N/A        | General purpose (production) computing, occasional GPU computing |
| qTRDHM     | arctrdhm001-arctrdhm003    | 5d 8h      | N/A      | 96   | 1.5TB  | N/A     | N/A         | N/A        | For job steps requiring in excess of 32 CPUs or 768GB memory     |

## GPU queue/partitions

| Partitions | Nodes                       | Time limit | Priority | CPUs | Memory | GPUs       | Limitations          | Preemption |
| ---------- | --------------------------- | ---------- | -------- | ---- | ------ | ---------- | -------------------- | ---------- |
| qTRDGPUH   | arctrddgxa001-arctrddgxa003 | 5d 8h      | high     | 40   | 512GB  | gpu:V100:8 | Max 8 GPUs per user  | N/A        |
|            | arctrdgn001-arctrdgn002     | 5d 8h      | high     | 40   | 192GB  | gpu:V100:4 | Max 8 GPUs per user  | N/A        |
| qTRDGPUM   | arctrddgxa001-arctrddgxa003 | 5d 8h      | medium   | 40   | 512GB  | gpu:V100:8 | Max 16 GPUs per user | suspend    |
|            | arctrdgn001-arctrdgn002     | 5d 8h      | medium   | 40   | 192GB  | gpu:V100:4 | Max 16 GPUs per user | suspend    |
| qTRDGPUL   | arctrddgx001-arctrddgxa003  | 5d 8h      | low      | 40   | 512GB  | gpu:V100:8 | N/A                  | suspend    |
|            | arctrdgn001-arctrdgn002     | 5d 8h      | low      | 40   | 192GB  | gpu:V100:4 | N/A                  | suspend    |
| qTRDGPU    | arctrdagn001-arctrdagn019   | 5d 8h      | N/A      | 64   | 512GB  | gpu:RTX:1  | N/A                  | N/A        |
|            | arctrdagn031-arctrdagn046   | 5d 8h      | N/A      | 128  | 512GB  | gpu:RTX:2  | N/A                  | N/A        |

## Special nodes

| Nodes                                        | CPUs | Memory | GPUs      | Purpose                                                                                                                                |
| -------------------------------------------- | ---- | ------ | --------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| {{site.data.trends.login_prompt}}.rs.gsu.edu | 0    | 1MB    | N/A       | Head node for submitting jobs on the cluster                                                                                           |
| arctrdcn017.rs.gsu.edu                       | 32   | 768GB  | N/A       | Tasks that support research, such as docker and other services/daemons, VS Code remote development, scheduled task, data transfer etc. |
| arctrdcn018.rs.gsu.edu                       | 32   | 768GB  | N/A       | Database server                                                                                                                        |
| {{site.data.trends.dev_node}}                | 4    | 62GB   | TITAN X:2 | GPU development & testing                                                                                                              |
| arctrdagn019.rs.gsu.edu                      | 64   | 512GB  | gpu:RTX:1 | GPU development & testing                                                                                                              |
| arctrdcn019-020.rs.gsu.edu                   | 32   | 768GB  | N/A       | BrainForge CPU Queue                                                                                                                   |
| arctrdagn020.rs.gsu.edu                      | 64   | 512GB  | gpu:RTX:1 | BrainForge GPU Queue                                                                                                                   |

## Using SLURM commands

```bash
# brief info and availability 
$ sinfo

# CPU and memory
$ sinfo -o "%24n %7P %.11T %.4c %.8m %14C %10e"

# CPU, memory and GPU
$ sinfo -O "nodehost:16,partition:.8,cpus:.8,memory:.8,cpusstate:.16,freemem:.8,gres:.16,gresused:.16,statelong:.8,time:.16"
```
