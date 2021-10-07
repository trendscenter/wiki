---
layout: default
title: Cluster & queue information
nav_order: 7
parent: Getting Started
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

```
Number     Manufacturer    Cores       Memory  GPUs            Name
20     Intel           32      768 GB                  trendscn0{01-20}
3      Intel           96      1.5 TB                  trendsmn00{1-3}
20     AMD             64      512 GB  1xNvidia 2080   trendsagn0{01-20}
4      Nvidia DGX-1    40      512 GB  8xNvidia V100   trendsdgx00{1-4}
2      Dell            40      192 GB  4xNvidia V100   trendsdgn00{1-2}
```

## CPU queue/partitions

| Partitions | Nodes                                           | Time limit | Priority | CPUs | Memory | GPUs         | Limitations                             | Preemption | Purpose                                                              |
|------------|-------------------------------------------------|------------|----------|------|--------|--------------|-----------------------------------------|------------|----------------------------------------------------------------------|
| qTRD       | trendscn001.rs.gsu.edu-trendscn016.rs.gsu.edu   | 5d 8h      | N/A      | 32   | 768GB  | N/A          | N/A                                     | N/A        | General purpose (production) computing                               |
| qTRDGPU    | trendsagn001.rs.gsu.edu-trendsagn020.rs.gsu.edu | 5d 8h      | N/A      | 64   | 512GB  | gpu:gforce:1 | N/A                                     | N/A        | General purpose (production) computing, occasional GPU computing     |
| qTRDEV     | trendscn019.rs.gsu.edu-trendscn020.rs.gsu.edu   | 5d 2h      | N/A      | 32   | 768GB  | N/A          | Max 6 CPUs per job, max 2 jobs per user | N/A        | Limited but guaranteed resources on demand for development & testing |
| qTRDHM     | trendsmn001.rs.gsu.edu-trendsmn003.rs.gsu.edu   | 5d 8h      | N/A      | 96   | 1.5TB  | N/A          | N/A                                     | N/A        | For job steps requiring in excess of 32 CPUs or 768GB memory         |

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

| Nodes                     | CPUs | Memory | GPUs         | Purpose                                                                                                                                |
|---------------------------|------|--------|--------------|----------------------------------------------------------------------------------------------------------------------------------------|
| trendslogin01.rs.gsu.edu  | 0    | 1MB    | N/A          | Head node for submitting jobs on the cluster                                                                                           |
| trendscn017.rs.gsu.edu    | 32   | 768GB  | N/A          | Tasks that support research, such as docker and other services/daemons, VS Code remote development, scheduled task, data transfer etc. |
| trendscn018.rs.gsu.edu    | 32   | 768GB  | N/A          | Database server                                                                                                                        |
| trendsgndev101.rs.gsu.edu | 4    | 62GB   | TITAN X:2    | GPU development & testing                                                                                                              |
| trendsagn019.rs.gsu.edu   | 64   | 512GB  | gpu:gforce:1 | GPU development & testing                                                                                                              |

## Using SLURM commands

```
# brief info and availability 
$ sinfo

# CPU and memory
$ sinfo -o "%24n %7P %.11T %.4c %.8m %14C %10e"

# CPU, memory and GPU
$ sinfo -O "nodehost:16,partition:.8,cpus:.8,memory:.8,cpusstate:.16,freemem:.8,gres:.16,gresused:.16,statelong:.8,time:.16"
```