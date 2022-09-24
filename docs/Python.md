---
layout: default
title: Python
nav_order: 2
parent: List of software
last_modified_date: 09/24/2022 11:58
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Using Python module

```
# Load Python module
$ module load python/3.9.9

$ which python3
/sysapps/ubuntu-applications/python/Python-3.9.9/Build/bin/python3

# run Python
$ python3 --version
Python 3.9.9
```

## Using Anaconda/Miniconda module

```
# Load miniconda module
$ module load miniconda3/4.12.0

$ which conda
/sysapps/ubuntu-applications/miniconda/4.12.0/miniconda3/bin/conda
$ which python
/sysapps/ubuntu-applications/miniconda/4.12.0/miniconda3/bin/python

# run Python
$ python3 --version
Python 3.9.9
```

## Installing your own Conda

```
# Login to a DEV node
$ ssh <campusID>@{{site.data.trends.dev_node}}

# Make a directory inside /data/users*/<your folder>
$ mkdir /data/users*/<your folder>/anaconda
$ cd /data/users*/<your folder>/anaconda
```

You have to grab the latest installer from [https://www.anaconda.com/distribution/](https://www.anaconda.com/distribution/).
In the following command, replace the Anaconda installer download URL and file name with the appropriate/latest one that you find above.

```
# Install Anaconda
$ wget https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh
$ chmod 755 Anaconda3-2021.05-Linux-x86_64.sh
$ ./Anaconda3-2021.05-Linux-x86_64.sh
# follow the instructions and complete install
```

## Create a Conda environment
```
$ conda create -n <env name> python=3.9

# Activate the Conda environment
$ conda activate <env name>
```

## Using your Conda environment in SLURM jobs

Add the following to the SLURM job submission script:

```
$ source <path to conda installation>/bin/activate <name/path of conda environment>
$ python script.py
```

See more examples [here](List_of_SLURM_scripts).

## Reinitialize conda

If you lose your default conda settings, such as the `(base)` environment from your `bash` prompt, you can always reinitialize `conda`.
To do that, navigate to your conda installation/bin directory, and run the `conda init` command.

```
$ cd /data/users1/salman/tools/miniconda4/bin/
$ conda init
```

Then log back in to the cluster.

## IPython: running Python scripts and commands interactively

```
# start ipython
$ ipython

# run a Python script
[$] %run hello.py

# list variables
[$] whos
```

## GPU and TensorFlow

[TBD]

## More information

[Python for Neuroimaging: A quick start](https://nilearn.github.io/introduction.html#python-for-neuroimaging-a-quick-start)