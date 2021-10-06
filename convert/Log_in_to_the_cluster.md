### Head/login node vs compute/worker nodes

You must be connected to the [GSU VPN](Configure_VPN "wikilink"), or in
the GSU network to log in to the cluster. Use the following command to
connect to the head/login node:

`$ ssh -XY `<campusID>`@trendslogin.gsu.edu`
`Warning: No xauth data; using fake authentication data for X11 forwarding.`
`Last login: Sun Oct  6 15:25:25 2019 from 131.96.253.116`
`[`<campusID>`@trendslogin01 ~]$`

`@trendslogin01` indicates that you are connected to the head/login
node. On the login node you can submit jobs, interact with the cluster,
edit files etc. But you should not run lengthy computations (more than a
few seconds) on the login node itself. For running computations, please
allocate resources on a compute/worker node which are accessible from
the head/login node:

`[`<campusID>`@trendslogin01 ~]$ srun -p qTRD -A PSYC0002 -v -n1 --mem=10g -t60 --pty --x11 /bin/bash`
`srun: defined options`
`srun: -------------------- --------------------`
`srun: account             : PSYC0002`
`srun: mem                 : 10G`
`srun: ntasks              : 1`
`srun: partition           : qTRD`
`srun: pty                 : set`
`srun: time                : 01:00:00`
`srun: verbose             : 1`
`srun: x11                 : all`
`srun: -------------------- --------------------`
`srun: end of defined options`
`srun: Waiting for nodes to boot (delay looping 450 times @ 0.100000 secs x index)`
`srun: Nodes trendscn013.rs.gsu.edu are ready for job`
`` srun: jobid 376466: nodes(1):`trendscn013.rs.gsu.edu', cpu counts: 1(x1) ``
`srun: CpuBindType=(null type)`
`srun: launching 376466.0 on host trendscn013.rs.gsu.edu, 1 tasks: 0`
`srun: route default plugin loaded`
`srun: Node trendscn013.rs.gsu.edu, 1 tasks started`
`[`<campusID>`@trendscn013 ~]$`

The above command will allocate 1 CPU on one of the nodes under `qTRD`
queue and 10GB of RAM on the said node (`trendscn013` in this case) for
60 minutes and start a `bash` session. See [this
page](Cluster_queue_information "wikilink") for more information about
the available queues.

For running GUI applications, depending on which SSH client or X-window
server you are using, you may need to use `-Y` or `-X`, e.g.:

`$ ssh -X `<campusID>`@trendslogin.gsu.edu`
`$ ssh -Y `<campusID>`@trendslogin.gsu.edu`

Or better yet, use both:

`$ ssh -XY `<campusID>`@trendslogin.gsu.edu`

### Windows Powershell

### Mobaxterm

Download MobaXterm from <https://mobaxterm.mobatek.net/>

![<File:Mobax2.png>](Mobax2.png "File:Mobax2.png")

![<File:Mobax3.png>](Mobax3.png "File:Mobax3.png")

### Putty

Download Putty from
<https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html>

![<File:Putty1.png>](Putty1.png "fig:File:Putty1.png")
![<File:Putty2.png>](Putty2.png "fig:File:Putty2.png")

![<File:Putty3.png>](Putty3.png "File:Putty3.png")

### Mac

### Git bash