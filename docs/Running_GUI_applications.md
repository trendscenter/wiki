---
layout: default
title: Running GUI applications
nav_order: 5
parent: Getting Started
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Install an X-window server

To display graphical interface from the cluster, you have to use X11 or
X-window server.

### Windows

On Windows, you have to setup and run
[Xming](https://sourceforge.net/projects/xming/),
[VcXsrv](https://sourceforge.net/projects/vcxsrv/) or
[MobaXterm](https://mobaxterm.mobatek.net/).

### Mac

On Mac, you can use [XQuartz](https://www.xquartz.org/). Note on
XQuartz: run the following in the terminal to fix issues with some GUI
applications:

`defaults write org.macosforge.xquartz.X11 enable_iglx -bool true`

Or, you may have to try downgrading to Xquartz version 2.7.8 [per this
thread](https://bugs.freedesktop.org/show_bug.cgi?id=96433).

### Linux

Linux supports X11 natively.

## Using MobaXterm and Xming

The following example shows how to run Matlab GUI, but you can run other
programs, e.g. AFNI the same way.

### Run MobaXterm

Log in to the cluster using MobaXterm:

![Mobax3]({{ site.baseurl }}/assets/images/mobax3.png)

### Run Xming

Download Xming from <https://sourceforge.net/projects/xming/>. Once run,
the Xming icon will be visible on the system tray:
![Xming]({{ site.baseurl }}/assets/images/xming.png)

### Run the application

#### Method 1 (via SLURM X11 option)

Run the following commands on MobaXterm while connected to the login
node:

```
$ module load Framework/Matlab2019b
$ srun -p qTRD -A PSYC0002 -v -n1 --mem=10g --export=TERM,HOME --pty --x11 /apps/Framework/MATLAB/R2019b/bin/matlab
```

![matlab]({{ site.baseurl }}/assets/images/mobax_matlab.png)

#### Method 2 (via interactive mode)

Run the following commands on MobaXterm while connected to the login
node:

```
$ srun -p qTRD -A PSYC0002 -v -n1 --mem=10g --pty --x11 /bin/bash 
$ module load Framework/Matlab2019b
$ matlab &
```

![matlab2]({{ site.baseurl }}/assets/images/mobax_matlab2.png)

![Matlab_xming]({{ site.baseurl }}/assets/images/matlab_xming.png)

## Using VNC viewer

[TBD]

## Using Git Bash

[Git for Windows](https://git-scm.com/downloads) provides a BASH
emulation used to run Git from the command line. \*NIX users should feel
right at home, as the BASH emulation behaves just like the "git" command
in LINUX and UNIX environments. The [Git for Windows SDK](https://github.com/git-for-windows/build-extra/releases) is a build
environment that includes all the tools necessary for developers who
want to contribute by writing code for Git for Windows.

Please set the following environment variable in Git Bash/SDK, and run
[Xming](https://sourceforge.net/projects/xming/) before connecting to the
cluster:

`export DISPLAY=localhost:0.0`