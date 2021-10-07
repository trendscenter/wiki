Visual Studio Code (https://code.visualstudio.com/) is a free coding
editor that helps you start coding quickly. Use it to code in any
programming language, without switching editors.

### Setting up for remote development

The Remote Development extension pack allows you to open any folder in a
container, on a remote machine, or in the Windows Subsystem for Linux
(WSL) and take advantage of VS Code's full feature set.

#### Install the Remote Development extension

-   Go to the extensions tab in VS Code.
-   Search for "remote".
-   Select the "Remote Development" extension and install it.

#### Configure SSH settings

-   Go to the "Remote explorer" tab in VS Code.
-   From the dropdown, select "SSH targets".
-   Click on the configure button next to "SSH targets".
-   Select an SSH configuration file, e.g. <user>/.ssh/config
-   Add the following configuration in the file that opens, then save
    it.

`host trends017`
`   HostName trendscn017.rs.gsu.edu`
`   user `<campusID>

-   `trends017` should now be available under SSH targets. You can right
    click and connect to it.

#### Tips

-   Once successfully connected, the bottom left corner of the VS Code
    window should indicate `SSH: trends017`, or whichever alias name you
    chose.
-   You should also be able to open a folder on the remote machine, open
    any file and edit them, open any image an view them. In addition, VS
    Code has extensions available for, for example, opening PDF or CSV
    files on the remote (and local) machine.
-   `trends017` is an alias, it can be anything.
    `trendscn017.rs.gsu.edu` must be a valid host name. Use one of the
    development nodes from the [Cluster queue
    information](Cluster_queue_information "wikilink") page. Do not use
    `trendslogin01.rs.gsu.edu` or `trendslogin.gsu.edu`
-   You may have to enter your password multiple times. To avoid this,
    set up SSH key authentication by following [Configure SSH for easy
    access to DEV
    machines](Configure_SSH_for_easy_access_to_DEV_machines "wikilink")
    or [this
    guide](https://docs.google.com/document/d/1C3IK38d5XiEIafktjJ6LxXVFMrj77unXm_9VAjGe3Ww/edit)

### SLURM jobs

#### Job submission

-   Open the VS Code integrated terminal (Ctrl+\`). It should be
    automatically connected to the remote machine (e.g.
    trendscn017.rs.gsu.edu).
-   Do `ssh trendslogin.gsu.edu`.
-   `cd` to the folder when you want to submit/start a SLURM job.
-   Use the VS Code editor pane (Ctrl+1) to set up or edit your job
    submission script.
-   Submit the SLURM job using `sbatch `<job submission script> command.
-   While on the login node, use `squeue`, `sinfo` etc. commands to
    monitor jobs.
-   DO NOT RUN ANY OTHER PROGRAM ON THE LOGIN NODE.

#### Interactive sessions

-   Open the VS Code integrated terminal (Ctrl+\`). It should be
    automatically connected to the remote machine (e.g.
    trendscn017.rs.gsu.edu).
-   Do `ssh trendslogin.gsu.edu`.
-   `cd` to the folder when you want to submit/start a SLURM job.
-   Start a SLURM interactive session, e.g.
    `srun -p qTRDEV -A PSYC0002 -v -n1 --pty -c4 --mem=10g /bin/bash`
-   Use the VS Code editor pane (Ctrl+1) to set up or edit your scripts,
    and execute them in the interactive session running on the VS Code
    terminal.
-   Once done, use `exit` command to exit from the interactive session,
    then from the login node.

#### Tips

-   Optional: start a tmux session on the remote machine (trends017),
    then start an interactive session. This way you can resume the
    session later even if you lose connection.
-   You can use tabs and multiple panels features of the VS Code
    integrated terminal to simultaneously run multiple sessions.

#### \[Python\] Selecting Interpreter and configuring Debugger

-   The full list of instructions can be found here:
    <https://code.visualstudio.com/docs/python/environments>
-   Install the Python extension for VScode
-   Once you are connected to the server, you can select your python
    interpreter (and conda environment) by hitting cntrl + shift + p (on
    windows) and selecting the "Python: Select Interpreter" option. This
    will show a list of your available interpreter installs and conda
    environments. Select one, and you should be good to go.