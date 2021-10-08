---
layout: default
title: Matlab
nav_order: 2
parent: List of software
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

### Running Matlab GUI

First, run an [X-window
server](Running_GUI_applications#Install_an_X-window_server),
and [connect to the login node with
SSH](Log_in_to_the_cluster). Then do one of the following:

Method 1 (via SLURM X11):

```
$ module load Framework/Matlab2019b
$ srun -p qTRDEV -A PSYC0002 -v -n1 -c1 --mem=10g --export=TERM,HOME --pty --x11 /apps/Framework/MATLAB/R2019b/bin/matlab
```

Method 2 (via interactive mode):

```
$ srun -p qTRDEV -A PSYC0002 -v -n1 -c1 --mem=10g --pty --x11 /bin/bash 
$ module load Framework/Matlab2019b
$ matlab &
```

### Executing a Matlab script in interactive mode

```
# start an interactive session
[<campusID>@trendslogin01 ~]$ srun -p qTRD -A PSYC0002 -v -c1 -t60 --pty --x11 /bin/bash                       
srun: defined options
srun: -------------------- --------------------
srun: account             : PSYC0002
...
[<campusID>@trendscn013 ~]$ cd /data/users1/salman/public/gsu_jobs_live/current/src/
[<campusID>@trendscn013 src]$ ls
array_aggregate_result_example.m  array_example.m  array_viz_example.m  parpool_example.m  simple_example.m
```

Execute the script:

```
[<campusID>@trendscn013 src]$ matlab -batch 'simple_example' -nodisplay
evaluating CalinskiHarabasz for K=2
cvi = 3.8406
...
Elapsed time is 3.439899 seconds.
Warning: MATLAB cannot use OpenGL for printing when started with the
'-nodisplay' option.
> In inputcheck
  In print (line 41)
  In print2array>read_tif_img (line 226)
  In print2array (line 180)
  In export_fig (line 606)
  In simple_example (line 50)
DONE!
```

### Use Matlab command prompt in bash

Start an interactive session:

```
[<campusID>@trendslogin01 ~]$ srun -p qTRD -A PSYC0002 -v -t60 --pty --x11 /bin/bash                       
srun: defined options
srun: -------------------- --------------------
srun: account             : PSYC0002
...
[<campusID>@trendscn013 ~]$ cd /data/users2/salman/public/gsu_jobs_live/current/src/
[<campusID>@trendscn013 src]$ ls
array_aggregate_result_example.m  array_example.m  array_viz_example.m  parpool_example.m  simple_example.m
```

Start Matlab without display:

```
[<campusID>@trendscn013 src]$ matlab -nodisplay

                                                                                             < M A T L A B (R) >
                                                                                   Copyright 1984-2019 The MathWorks, Inc.
                                                                              R2019a Update 4 (9.6.0.1150989) 64-bit (glnxa64)
                                                                                                June 26, 2019


To get started, type doc.
For product information, visit www.mathworks.com.
```

Use the command prompt like you normally would in a GUI:

```
>> ls
array_aggregate_result_example.m  array_viz_example.m  simple_example.m
array_example.m                   parpool_example.m
```

Execute a script:

```
>> simple_example
evaluating CalinskiHarabasz for K=2
cvi = 3.8406
...
Elapsed time is 2.567810 seconds.
Warning: MATLAB cannot use OpenGL for printing when started with the
'-nodisplay' option.
> In inputcheck
  In print (line 41)
  In print2array>read_tif_img (line 226)
  In print2array (line 180)
  In export_fig (line 606)
  In simple_example (line 50)
DONE!
```

Check variables in the workspace:

```
>> whos
  Name               Size             Bytes  Class                                         Attributes

  K                  1x13               104  double
  c                  1x1                  8  double
  criteria           1x3                414  cell
  cvi                3x13               312  double
  data_path          1x8                 16  char
  dfnc            1000x28            224000  double
  i                  1x1                  8  double
  labels          1000x1               8000  double
  limit_rows         1x1                  8  double
  outpath            1x11                22  char
  runpath            0x0                  0  char
  t1                 1x1             225236  clustering.evaluation.SilhouetteEvaluation

>>
```

### Debug Matlab in command line

Please see
[this](https://www.mathworks.com/help/matlab/ref/dbstep.html#buyrwwi-4).

### Parallel pools, multi-threading and memory considerations

Please see [this](Choosing_job_resources).

### More on memory optimization

-   [Strategies for Efficient Use of Memory](https://www.mathworks.com/help/matlab/matlab_prog/strategies-for-efficient-use-of-memory.html)
-   [Performance and Memory](https://www.mathworks.com/help/matlab/performance-and-memory.html?s_tid=CRUX_lftnav)