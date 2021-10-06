## Jupyter as a SLURM job

**Create an SBATCH `JobSubmit.sh` script**

*on the login node*

`#!/bin/bash`
`#SBATCH -N 1`
`#SBATCH -n 1`
`#SBATCH -c 1`
`#SBATCH --mem=10g`
`#SBATCH -p qTRD`
`#SBATCH -t 60`
`#SBATCH -J `<job name>
`#SBATCH -e error%A.err`
`#SBATCH -o out%A.out`
`#SBATCH -A PSYC0002`
`#SBATCH --mail-type=ALL`
`#SBATCH --mail-user=`<email address>
`#SBATCH --oversubscribe`

`sleep 10s`

`export OMP_NUM_THREADS=1`
`export MODULEPATH=/apps/Compilers/modules-3.2.10/Debug-Build/Modules/3.2.10/modulefiles/`
`echo $HOSTNAME >&2 `

`source `<path to conda installation>`/bin/activate `<name/path of conda environment>

`jupyter lab --ip=0.0.0.0 --port=8888`

`sleep 30s`

Note: If port `8888` is not available, change it to something else
higher, e.g., `8889, 8890` etc.

**Submit the job**

*on the login node*

`$ sbatch JobSubmit.sh`

**Find the allocated node and Jupyter token/URL**

*on the login node*

Wait a few minutes for Jupyter to start. Then observe the log files
`out`<jobid>`.out, error`<jobid>`.err`:

`$ cat *`<jobid>`*`
`trendscn010.rs.gsu.edu`
`[I 15:47:14.720 LabApp] JupyterLab extension loaded from /data/users2/salman/tools/miniconda4/envs/py37/lib/python3.7/site-packages/jupyterlab`
`[I 15:47:14.720 LabApp] JupyterLab application directory is /data/users2/salman/tools/miniconda4/envs/py37/share/jupyter/lab`
`[I 15:47:14.763 LabApp] Serving notebooks from local directory: /data/users2/salman/public/jupyter`
`[I 15:47:14.763 LabApp] Jupyter Notebook 6.1.6 is running at:`
`[I 15:47:14.763 LabApp] `[`http://trendscn010.rs.gsu.edu:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744`](http://trendscn010.rs.gsu.edu:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744)
`[I 15:47:14.763 LabApp]  or `[`http://127.0.0.1:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744`](http://127.0.0.1:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744)
`[I 15:47:14.763 LabApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).`
`[W 15:47:14.888 LabApp] No web browser found: could not locate runnable browser.`
`[C 15:47:14.889 LabApp]`

`    To access the notebook, open this file in a browser:`
`        `[`file:///home/users/msalman/.local/share/jupyter/runtime/nbserver-254872-open.html`](file:///home/users/msalman/.local/share/jupyter/runtime/nbserver-254872-open.html)
`    Or copy and paste one of these URLs:`
`        `[`http://trendscn010.rs.gsu.edu:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744`](http://trendscn010.rs.gsu.edu:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744)
`     or `[`http://127.0.0.1:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744`](http://127.0.0.1:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744)
`[I 15:47:52.321 LabApp] 302 GET /?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744 (10.245.10.57) 0.970000ms`
`[W 15:47:53.938 LabApp] Could not determine jupyterlab build status without nodejs`

As we can see, the job is allocated on `trendscn010.rs.gsu.edu` and the
URL is
[`http://127.0.0.1:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744`](http://127.0.0.1:8888/?token=ba96539d0781ca6d191db39ce01cea4256def026d5da4744).

**Create an SSH tunnel**

*On your local machine*

`$ ssh -L8888:trendscn010.rs.gsu.edu:8888 `<campusID>`@trendscn017.rs.gsu.edu`

Make sure to change `trendscn010.rs.gsu.edu` and `8888` to the
appropriate host/port.

**Access Jupyter**

*On your local machine*

Open a browser window and browse to the Jupyter URL noted previously.

**Cleaning up**

Make sure to shut down Jupyter from the browser once you are done. If
that is not possible for some reason and the resource is still
allocated, you can use one of the following commands on the login node
to end the job:

`$ scancel `<jobid>
`$ scancel -u `<campusID>