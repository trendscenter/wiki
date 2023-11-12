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

## Setting up the Python environment

### Using The Python module

```
# Load Python module
$ module load python/3.9.9

$ which python3
/sysapps/ubuntu-applications/python/Python-3.9.9/Build/bin/python3

# create a virtual environment
$ mkdir -p /data/users*/<your directory>/<name of env>
$ python -m <name of env> /data/users*/<your directory>/<name of env>

# activate the environment
$ source /data/users*/<your directory>/<name of env>/venv/bin/activate

# run Python
$ python --version
```

### Using Anaconda/Miniconda module

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

# Create a Conda environment
$ conda create -n <env name> python=3.9

# Activate the Conda environment
$ conda activate <env name>
```

### Installing your own Conda

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

# Create a Conda environment
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

### Support graphics output in remote sessions

A terminal that is compatible with mrpeek seems to be sufficient, but
we only tested this on Mac OS's `iterm2` and Ubuntu's `mlterm`
* ssh to a dev machine from iterm2 or mlterm
* activate your environment
* install the following dependencies
```
pip install gr
pip install ipython
pip install matplotlib==3.2.2 # newer versions break gr (11/11/2023)
```
* run ipython as follows 
```env GKS_WSTYPE=iterm MPLBACKEND=module://gr.matplotlib.backend_gr ipython```
* To test that is worked run this code inside `ipython`:
```
import numpy as np
import pylab as plt
plt.imshow(np.random.randn(5,5), interpolation=None)
plt.show()
```

## GPU

To use GPUs in your Python scripts, first create an environment using any of the methods described above.
Then go to [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/) and configure your installation, including CUDA toolkit.
Following is an example of the process.

```
$ ssh {{site.data.trends.login_node}}
$ module load miniconda3/4.12.0
$ conda init

# Log back in to have base env loaded.
$ ssh {{site.data.trends.login_node}}

# start an interactive session
$ srun -p qTRDGPUH -A trends53c17 -v -n1 --pty -c3 --mem=60g --gres=gpu:V100:1 /bin/bash

# set up new environment
$ module load miniconda3/4.12.0
$ conda create -n testenv1 python=3.9
$ conda activate testenv1

# install GPU essentials for PyTorch
$ conda install pytorch torchvision torchaudio cudatoolkit=11.6 -c pytorch -c conda-forge
```

## More information

[Python for Neuroimaging: A quick start](https://nilearn.github.io/introduction.html#python-for-neuroimaging-a-quick-start)
