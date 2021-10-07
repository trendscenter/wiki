---
layout: default
title: File transfer with SCP
nav_order: 3
parent: Storage Guide
---
scp - secure copy (remote file copy program) command copies files
between hosts on a network (https://linux.die.net/man/1/scp).

### Examples

```
# transfer a file from remote to local
$ scp <campusID>@trendslogin.gsu.edu:<full path to file on remote> .

# transfer a file from local to remote
$ scp <file_name> <campusID>@trendslogin.gsu.edu:<full path to directory on remote>

# transfer a directory from remote to local
$ scp -r <campusID>@trendslogin.gsu.edu:<full path to directory on remote> .

# transfer a directory from local to remote
$ scp -r <directory_name> <campusID>@trendslogin.gsu.edu:<full path to directory on remote>
```
