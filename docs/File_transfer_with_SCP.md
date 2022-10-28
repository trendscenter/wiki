---
layout: default
title: File transfer with SCP
nav_order: 3
parent: Storage Guide
---
scp - secure copy (remote file copy program) command copies files between hosts on a network [https://linux.die.net/man/1/scp](https://linux.die.net/man/1/scp).

### Examples

Following examples assume you have [SSH settings configured](Configure_SSH_for_easy_access_to_DEV_machines).

```
# transfer a file from remote to local
$ scp <campusID>@{{site.data.trends.dev_alias}}:<full path to file on remote> .

# transfer a file from local to remote
$ scp <file_name> <campusID>@{{site.data.trends.dev_alias}}:<full path to directory on remote>

# transfer a directory from remote to local
$ scp -r <campusID>@{{site.data.trends.dev_alias}}:<full path to directory on remote> .

# transfer a directory from local to remote
$ scp -r <directory_name> <campusID>@{{site.data.trends.dev_alias}}:<full path to directory on remote>
```

### WinSCP

You can also use [WinSCP](https://winscp.net/eng/index.php) or [FileZilla](https://filezilla-project.org/download.php?show_all=1) to transfer files visually.

![Filezilla-1]({{ site.baseurl }}/assets/images/filezilla.png)


