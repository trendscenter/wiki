---
layout: default
title: mriqc
nav_order: 2
parent: List of software
---
MRIQC: Automated Quality Control and visual reports for Quality
Assessment of structural (T1w, T2w) and functional MRI of the brain

```
# Load FSL
$ module load Image_Analysis/FSL5.0.11

# Load AFNI
$ module load Image_Analysis/AFNI

# Load ANTS
$ export ANTSPATH=/trdapps/linux-x86_64/bin/ants/bin
$ export PATH=${ANTSPATH}:$PATH

# Load mriqc
$ module load Image_Analysis/mriqc

# Run mriqc
$ mriqc
```
