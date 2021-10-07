---
layout: default
title: Singularity & docker
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

This page is written by Eric Verner.

## Docker

[Docker](https://www.docker.com) is the most popular containerization
technology in use today. Docker offers OS-level virtualization, allowing
developers to package libraries, code, and the operating system together
in one image, which can be programmatically created on the fly. This
means that software will run the same on any platform that can run
Docker, enabling users to easily share code with others.
Containerization has been impactful in the neuroimaging community, as
neuroimaging pipelines often require many libraries that can be
difficult to install on one's computer. [BIDS
apps](https://bids-apps.neuroimaging.io/about/) and
[Neurodocker](https://github.com/ReproNim/neurodocker) are good examples
of Docker images made for neuroimaging. Docker is also commonly used
with container orchestration technologies such as
[docker-compose](https://docs.docker.com/compose/) and
[Kubernetes](https://kubernetes.io).

### Caveats

-   Docker is only allowed on development nodes (currently
    `trendscn017.rs.gsu.edu` and `trendsgndev101.rs.gsu.edu`, but check
    [Cluster_queue_information](Cluster_queue_information)
    for updates). Because operations are run as root inside of a
    container, Docker is seen as a security vulnerability and is often
    not allowed on high-performance computing (HPC) systems. To run a
    Docker container using Slurm, you must convert it to a Singularity
    image first. See the section below on building Singularity images to
    learn how to do this.

<!-- -->

-   Docker runs on Linux, Mac, and Windows Professional but requires
    additional work to install on Windows.

### How to run a Docker image on the cluster?

Docker images must be either pulled from another source, such as
[DockerHub](https://hub.docker.com), or built locally (see next
section). After the image has been built, you can find it by typing

    docker image ls

To run a command inside a container, use a `docker run` command:

    docker run -it myimage bash

This command opens up an interactive bash session into the container.
Note that `docker run` creates a container, which can be thought of as a
live instance of an image. The terms "container" and "image" are often
used interchangeably, though.

If a Docker container has been started with a persistent process, like a
server, then it can be accessed using a [docker
exec](https://docs.docker.com/engine/reference/commandline/exec/)
command.

### How to build a Docker image on the cluster

Docker images are built using Dockerfiles, which can be thought of as
recipes. Please see this
[page](https://docs.docker.com/get-started/part2/#sample-dockerfile) for
more information about how to use Dockerfiles. An example build command
is

     docker build . -t myimage:latest

This builds a Docker image using the code in the current working
directory containing a Dockerfile and tagging it with the name
`myimage:latest`.

### How to share data with a Docker container

Docker uses volumes to share data between the host system and the
container. To share a folder with a container, use a command like this:

    docker run -v /folder/on/host:/folder/in/container myimage -it bash

To share multiple folders, use multiple `-v` flags.

    docker run \
    -v /first/folder/on/host:/first/folder/in/container \
    -v /second/folder/on/host:/second/folder/in/container \
    myimage -it bash

### GPU usage

It is possible to use a host system's GPU inside a Docker container. The
Docker image must be built using an
[nvidia/cuda](https://hub.docker.com/r/nvidia/cuda/) image as its base
image. Note that the version of CUDA on the host should match that
inside the image. Actually, different versions may be compatible, but
the relationship is complicated, so it is easier to use the same
versions when possible. After you have built your image, you can run a
command like so

     docker run --gpus all nvidia/cuda:10.2-base nvidia-smi

This command runs `nvidia-smi` on the `cuda:10.2-base` image. The
`--gpus` flag must be used to expose the host system's GPUs inside the
container, and `--gpus all` allows the container to use all the GPUs on
the host system. For more information, see the official [NVIDIA Docker
GitHub page](https://github.com/NVIDIA/nvidia-docker).

## Singularity

[Singularity](https://sylabs.io/singularity/) is a containerization
technology that is friendly for HPC systems. Commands can be run inside
Singularity as a non-root user. This has made it a popular choice at
universities and within the neuroimaging community.

### How to run a Singularity container on the cluster

You can interact with a Singularity image using the `exec`, `run`, or
`shell` commands.

To open up a shell into a container, use `singularity shell`.

To run a Singularity container using its run script, use
`singularity run`

To run any other command inside a Singularity container, use
`singularity exec`

See this [page](https://sylabs.io/guides/3.5/user-guide/cli.html) for
more details.

### How to build a Singularity image on the cluster

Singularity images can be built from scratch using a [definition
file](https://sylabs.io/guides/3.5/user-guide/definition_files.html) or
can be built from existing Docker or Singularity images from a local or
remote library, such as Singularity Hub or Docker Hub. They can also be
built from locally cached Docker images. For more information, see this
[page](https://sylabs.io/guides/3.5/user-guide/build_a_container.html).

For example, to build from the `lolcow` image from the Singularity
Library, use this command:

     singularity pull lolcow.sif library://sylabs-jms/testing/lolcow

To build from Docker Hub, use this command:

     singularity build lolcow.sif docker://godlovedc/lolcow

If pulling from a private Docker Hub repository, you must enter your
Docker credentials, either interactively or with environment variables
(see
[here](https://sylabs.io/guides/3.5/user-guide/singularity_and_docker.html#authentication-via-environment-variables)).

To build from a locally cached Docker image, use this command:

     singularity build lolcow.sif docker-daemon://godlovedc/lolcow

Note that Docker and Singularity must be available on the same system
for this to work.

### Caveats

-   Several users have had problems building Singularity images on the
    cluster. The current recommended approach is to build the image on
    the dev node (`trendscn017`) inside of the `/data/singtmp/`
    directory. Also, use a local cache to build the container, where
    `username` is your username, as shown below. This will build the
    container inside of `/data/singtmp/username`

<!-- -->

    ssh trendscn017.rs.gsu.edu
    cd /data/singtmp
    mkdir -p username/cache
    cd username
    SINGULARITY_CACHEDIR=/data/singtmp/username/cache
    module load SysTools/Singularity3.5.2
    singularity pull ...

-   Singularity only runs natively on Linux. Singularity Desktop can run
    on Mac OS, but it lacks some features such as building from Docker
    Hub. Singularity can be run using a Linux VM on Mac or Windows,
    though (see
    [here](https://sylabs.io/guides/3.2/user-guide/installation.html#install-on-windows-or-mac)).

### How to share data with a Singularity container

Singularity lets you share folders from the host system with the
container using the `--bind` flag. In the example below, the `/opt`
folder on the host is bound to the same folder inside the container, and
the `/data` folder on the host system is bound to the `/mnt` folder in
the container called `my_container.sif`.

    singularity shell --bind /opt,/data:/mnt my_container.sif

This also works for `run` and `exec` commands. Any changes made inside
the container during this command will persist on the host system after
the command is complete, so be careful.

Singularity also mounts your home folder by default, which may lead to
surprising results. Use the `--containall` flag to stop this from
happening. For example,

    singularity shell --bind /opt,/data:/mnt --containall my_container.sif

See this
[page](https://sylabs.io/guides/3.5/user-guide/bind_paths_and_mounts.html)
for more details.

### GPU usage

Singularity containers can utilize GPUs on the host system. The `--nv`
flag must be used with a container that has the Nvidia runtime
installed, as shown below.

    singularity pull docker://tensorflow/tensorflow:latest-gpu
    singularity run --nv tensorflow_latest-gpu.sif

See this [page](https://sylabs.io/guides/3.5/user-guide/gpu.html) for
more details on GPU support.