---
layout: default
title: Monitor CPU and memory
nav_order: 4
parent: SLURM Overview
last_modified_date: 2026-10-14 00:00
---
On a compute node you get the machine to yourself. So you can just watch it live.

## `top`

The simplest tool. It is already installed.

```
$ top
```

- Press `1` to show one line per CPU.
- Press `q` to quit.

`top` shows two numbers per process that matter most:

- `%CPU` - how much CPU the process uses.
- `%MEM` - how much memory the process uses.

Use this if you just want a quick look.

## `htop`

The same idea as `top`, but much easier to read. It has colors, bars, and
you can click a column to sort by it.

```
$ htop
```

- Press `F2` or `F10` to quit.
- Press `F6` to change the sort column.
- `F4` filters by process name.
- `F5` shows the tree, so you can see which process started which.

If you see `htop: command not found`, add `/usr/bin` to your path, for
example `export PATH=/usr/bin:$PATH`.

Use `htop` if `top` is too hard to read.

## `nvtop`

Use this on a GPU node.

```
$ /trdapps/linux-x86_64/bin/nvtop
```

It shows one row per GPU, plus how much memory and how much compute each
process uses on the GPU. See the [nvtop](Nvtop) page.

## Lightweight options

These use very little CPU, so they are fine to leave running.

### `uptime`

How busy the node has been over the last 1, 5 and 15 minutes.

```
$ uptime
```

### `free -h`

How much memory is free, and how much is in the page cache.

```
$ free -h
```

- `available` is the number you care about.
- If `available` is close to zero, your job will be killed.

### `ps`

A single snapshot of the processes. No live view, so it costs almost nothing.

```
$ ps aux --sort=-%mem | head
```

This shows the 10 processes that are using the most memory.

## Note

Run these inside your SLURM job or inside your interactive session.

Do not run them on the login node for a long time. See
[Cluster do's & don'ts](Cluster_do's_&_don'ts).

## More background

See [Resource usage](https://docs.ycrc.yale.edu/clusters-at-yale/job-scheduling/resource-usage/)
for a longer explanation of how CPU and memory requests map to what you
actually get.
