---
layout: default
title: AFNI
nav_order: 2
parent: List of software
---
Analysis of Functional NeuroImages (AFNI) is an open-source environment
for processing and displaying functional MRI data—a technique for
mapping human brain activity.

### Login to the cluster

`$ ssh -XY <campusID>@trendslogin.gsu.edu`

### Start an interactive bash session with `--x11` option

**You also need to run an X-window server on your machine.**

`$ srun -p qTRDEV -A <slurm_account_code> -v -n1 --mem=10g -t60 --pty --x11 /bin/bash`

### Load the `AFNI` module

`$ module load Image_Analysis/AFNI`

### Run `AFNI`

`$ afni &`