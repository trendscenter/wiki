---
layout: default
title: FSL
nav_order: 2
parent: List of software
---
FSL is a comprehensive library of analysis tools for FMRI, MRI and DTI
brain imaging data.

```
# Login to the cluster
$ ssh -XY <campusID>@trendslogin.gsu.edu

# Start an interactive bash session with --x11 option===
# You also need to run an X-window server on your machine.
$ srun -p qTRD -A PSYC0002 -v -n1 -c1 --mem=10g -t60 --pty --x11 /bin/bash

# Find the appropriate version by running module avail command 
$ module avail fsl

# Load the FSL module
$ module load Image_Analysis/FSL5.0.11

# Run FSL
$ fsl
```
