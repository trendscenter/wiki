---
layout: default
title: GIFT
nav_order: 2
parent: List of software
last_modified_date: 10/5/2022 21:49
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

GIFT is an application supported by the NIH under grant 1RO1EB000840 to Dr. Vince Calhoun and Dr. Tulay Adali. 
It is a MATLAB toolbox which implements multiple algorithms for independent component analysis and blind source separation of group (and single subject) functional magnetic resonance imaging data.

## Using GIFT GUI

### Run Matlab GUI

To use Matlab GUI, select Matlab from the TReNDS interactive apps on [https://hemera.rs.gsu.edu/](https://hemera.rs.gsu.edu/).

### Add GIFT path

`>> addpath(genpath('/trdapps/linux-x86_64/matlab/toolboxes/GroupICATv4.0b/'))`

### Run GIFT

`>> gift`

![Gift]({{ site.baseurl }}/assets/images/gift.png)

### Example analysis: Group ICA on auditory oddball data

Change to the data directory and create a folder. Then click "Setup ICA
Analysis" in GIFT and select the output folder.

```
$ cd /data/users2/salman/mind/data/
$ mkdir ica_example/
```

![Gift_select]({{ site.baseurl }}/assets/images/gift_select.png)

Select all subject data and all the ICA options.

![Gift_subject]({{ site.baseurl }}/assets/images/Gift_subject.png)

Click the "Run Analysis" button in the GIFT window and start the
analysis.

![Gift_run]({{ site.baseurl }}/assets/images/gift_run.png)

Once analysis is done, visualize the output.

![gift_result]({{ site.baseurl }}/assets/images/gift_result.png)

## Using GIFT Batch Scripts

Create the following batch script `gift_batch.m`:

```
inputFile = '/path/to/input/file';
addpath( genpath( '/trdapps/linux-x86_64/matlab/toolboxes/GroupICATv4.0b/icatb/' ) )
icatb_batch_file_run(inputFile)
```

Sample batch input files are located in the GIFT toolbox folder, e.g.: `/trdapps/linux-x86_64/matlab/toolboxes/GroupICATv4.0c/icatb/icatb_batch_files/Input_spatial_ica.m`. Please make a copy of it and make necessary changes.

Execute the script using the following commands (in a SLURM job script
or interactive node):

```
$ module load matlab/R2022a
$ matlab -batch 'gift_batch'
```

### Serial/Parallel Mode

If you select `parallel_info.mode = 'serial';` in the GIFT batch input
file, you can increase the number of allocated CPUs in the SLURM job
script for faster analysis, e.g.

```
#SBATCH -c 5
#SBATCH --mem=80g
```

If you select `parallel_info.mode = 'parallel';` in the GIFT batch input
file, you can set the number of parallel pools equal to the number of
allocated CPUs (in the `#SBATCH -c` directive) in the SLURM job script,
e.g.

```
# in job script 
...
#SBATCH -c 5

# in batch input file
...
parallel_info.num_workers = 5;
```

## Memory considerations

Note that GIFT tells you the amount of memory you need to run the
analysis. Please see [this section](Choosing_job_resources)
for how to properly configure SLURM and Matlab for running the analysis
successfully.