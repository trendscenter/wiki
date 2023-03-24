---
layout: default
title: FSL
nav_order: 2
parent: List of software
last_modified_date: 10/5/2022 21:35
---
FSL is a comprehensive library of analysis tools for FMRI, MRI and DTI
brain imaging data.

To use FSL GUI, select FSL from the TReNDS interactive apps on [https://hemera.rs.gsu.edu/](https://hemera.rs.gsu.edu/).

## instruction for srun/sbatch

```
# Find the appropriate version by running module avail command
$ module avail fsl

# Load the FSL module
$ module load Image_Analysis/FSL5.0.11

# Run FSL
$ fsl
```


If the above is not working or buggy, try the following instead.

```
FSLDIR=/trdapps/linux-x86_64/bin/fsl
. ${FSLDIR}/etc/fslconf/fsl.sh
PATH=${FSLDIR}/bin:${PATH}
export FSLDIR PATH
# Run FSL
$ fsl
$ fsleyes
```
