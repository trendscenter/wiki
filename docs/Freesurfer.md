---
layout: default
title: Freesurfer
nav_order: 2
parent: List of software
---
FreeSurfer is a software package for the analysis and visualization of
structural and functional neuroimaging data from cross-sectional or
longitudinal studies.

```
# Login to the cluster
$ ssh -XY <campusID>@trendslogin.gsu.edu

# Start an interactive bash session with --x11 option
# You also need to run an X-window server on your machine.
$ srun -p qTRD -A PSYC0002 -v -n1 -c1 --mem=10g -t60 --pty --x11 /bin/bash

# Load the Freesurfer module and setup environment
$ module load Image_Analysis/Freesurfer
$ source $FREESURFER_HOME/SetUpFreeSurfer.sh
```