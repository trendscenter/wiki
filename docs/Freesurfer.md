---
layout: default
title: Freesurfer
nav_order: 2
parent: List of software
last_modified_date: 10/5/2022 21:49
---
FreeSurfer is a software package for the analysis and visualization of
structural and functional neuroimaging data from cross-sectional or
longitudinal studies.

### Running Freesurfer GUI

To use Freesurfer GUI, select TReNDS Interactive desktop from under TReNDS interactive apps on [https://hemera.rs.gsu.edu/](https://hemera.rs.gsu.edu/). 
Once the session is launched, open a terminal and run the following commands for loading the module and setup. 

```
$ module load freesurfer/7.3.2
$ source $FREESURFER_HOME/SetUpFreeSurfer.sh
```

Then you should be able to use any GUI application.

```
$ freeview
```

### Running Freesurfer in terminal

```
# Login to the cluster
$ ssh -XY <campusID>@{{site.data.trends.login_node}}

# Start an interactive bash session
$ srun -p qTRD -A <slurm_account_code> -v -n1 -c1 --mem=10g -t60 --pty /bin/bash

# Load the Freesurfer module and setup environment
$ module load freesurfer/7.3.2
$ source $FREESURFER_HOME/SetUpFreeSurfer.sh
```

