---
layout: default
title: Storage Guide
nav_order: 3
has_children: true
last_modified_date: 09/24/2022 11:20
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Home

-   Home directory is where you log in to.
-   Home directory quota is limited, it is not advisable to put analysis data here. Please use `/data/users*/< your directory >` instead.
-   You can `ls ~` from anywhere to quickly switch to the home directory. 
`pwd` will show full path to the current location.

## TReNDS storage

### Users `/data/users1` and `/data/users2`

TReNDS center members own and can keep their data in `/data/users/2`<campusID> directory.

{: .important}
The user storage is limited and shared between all members of the lab. 
So please make sure to clean up your user directory in `/data/users*/< username >` periodically and remove any data that are either duplicate (available at another location on the cluster) or no longer needed.

{: .tip}
Use `df -h` command to have a look at the overall storage capacity of the cluster.
You can use `du` options such as `du -h --max-depth=1 | sort` to get more detail information.

{: .tip}
Use `dust` to get a visual description of what's inside a directory.
Make sure `/trdapps/linux-x86_64/bin/` is in your path to have the command working.

### Mialab `/data/mialab2`, Analysis `/data/analysis` & Collaboration `/data/collaboration`

MIALab, collaboration and auto-analysis data are stored here.

### Neuromark `/data/qneuromark` and `/data/neuromark2`

Neuromark datasets are located here.
Qumulo storage (`/data/qneuromark`) capacity, usage, quota etc. can be viewed at [trendsq1.gsu.edu](https://trendsq1.gsu.edu/).

### `/trdapps`

Some specific software (which are not available as modules, such as GIFT) are installed in `/trdapps`.
Add `/trdapps/linux-x86_64/bin/` to your path to take advantage of these tools:

`export PATH=/trdapps/linux-x86_64/bin/:$PATH`

### `/scratch`

This is for short-term data, great for working environment such as moving files during a job, storing data to be used in a job, or storing generated files from a job. 
Transfer output and resulting data off `/scratch` after job is executed.

### `/raid`

It is a local SSD on the DGX machines for fast data transfer.

### `/dev/shm`

You can directly load data on to memory by using [`/dev/shm`](https://www.cyberciti.biz/tips/what-is-devshm-and-its-practical-usage.html) for very fast processing. 
It is recommended to reserve a full node when using `/dev/shm` and take special precautions to prevent out-of-memory errors.

{: .caution}
Be very careful when using `/dev/shm` because overloading this may destroy the node.