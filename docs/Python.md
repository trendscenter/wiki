---
layout: default
title: Python
nav_order: 2
parent: List of software
---
## Using Python module

`# Load Python module`
`$ module load Compilers/PythonIntel3.6 `

`$ which python3`
`/apps/Compilers/Intel-Python/intelpython3/bin/python3`

`# run Python`
`$ python3 --version`
`Python 3.6.3 :: Intel Corporation`

Note: use `python3` instead of `python` command.

## Using your own Conda environment

`# Login to a DEV node`
`$ ssh `<campusID>`@trendscn017.rs.gsu.edu`

`# Make a directory inside /data/users2/`<your folder>
`$ mkdir /data/users2/`<your folder>`/anaconda`
`$ cd /data/users2/`<your folder>`/anaconda`

`# Install Anaconda`
`# You have to grab the latest installer from `[`https://www.anaconda.com/distribution/`](https://www.anaconda.com/distribution/)
`$ wget `[`https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh`](https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh)
`$ chmod 755 Anaconda3-2021.05-Linux-x86_64.sh`
`$ ./Anaconda3-2021.05-Linux-x86_64.sh`

`# Create a Conda environment`
`$ conda create -n `<env name>` python=3.7`

`# Activate the Conda environment`
`$ conda activate `<env name>

## Using your Conda environment in SLURM jobs

Add the following to the SLURM job submission script:

`$ source `<path to conda installation>`/bin/activate `<name/path of conda environment>
`$ python script.py`

See more examples [here](List_of_SLURM_scripts).

## IPython: running Python scripts and commands interactively

`# start ipython`
`$ ipython`

`# run a Python script`
`[$] %run hello.py`

`# list variables`
`[$] whos`

## GPU and TensorFlow

## More information

[Python for Neuroimaging: A quick
start](https://nilearn.github.io/introduction.html#python-for-neuroimaging-a-quick-start)