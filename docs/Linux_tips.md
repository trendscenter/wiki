---
layout: default
title: Linux tips
nav_order: 8
parent: New User Guide
---
### Learn bash in 15 minutes

<https://learnxinyminutes.com/docs/bash/>

### How much free space is there in the server?

`$ df -h`
`Filesystem               Size  Used Avail Use% Mounted on`
`devtmpfs                  47G     0   47G   0% /dev`
`tmpfs                     47G     0   47G   0% /dev/shm`
`tmpfs                     47G  455M   46G   1% /run`
`tmpfs                     47G     0   47G   0% /sys/fs/cgroup`
`/dev/sda2                218G  9.8G  209G   5% /`
`/dev/sda1               1014M  228M  787M  23% /boot`
`/dev/sdb1                9.1T  6.7T  2.5T  74% /data/usb-drive`
`gfs01ib:/usersvol01.tcp   15T  3.7T   12T  25% /home/users`
`gfs01ib:/mialab.tcp      330T  267T   64T  81% /data/mialab`
`gfs01ib:/trdapps.tcp      30T  346G   30T   2% /trdapps`
`gfs01ib:/collab.tcp      300T  286T   15T  96% /data/analysis`

Above example shows 64TB free space in /data/mialab and 15TB in
/data/analysis, which are primarily used for research data and tools. It
also shows 12TB free space in the home directory.

### Find information about the system

`# Processors `
`$ lscpu`

`# Memory`
`$ free -h`

`# Processors and memory`
`$ top`
`$ htop`

`# GPUs`
`$ nvidia-smi`
`$ nvtop # see software page for details`

### How big is <some directory>?

`$ cd `<some directory>
`$ du -sh`

`# get size of each child directory`
`$ du -h --max-depth=1`

### Display help about a command

`$ `<command>` --help`
`$ man `<command>

### `ls` tricks

`# list extra info about files`
`$ ls -l`

`# list hidden files along with extra info`
`$ ls -al`

`# list files in order of date modified`
`$ ls -lt`
`$ ls -ltr`

`# list files in order of size`
`$ ls -Sl`
`$ ls -Slr`

`# how many file/folders in a directory`
`$ ls | wc -l`

`# how many file/folders with `<something>` in the name in a directory`
`$ ls | grep -i *`<something>`* | wc -l`

### Text file tricks

`# view contents of a file`
`$ cat `<filename>

`# search contents of a file`
`$ cat `<filename>` | grep `<something>

`# case-insensitive search`
`$ cat `<filename>` | grep -i `<something>

`# inverse search`
`$ cat `<filename>` | grep -v `<something>

`# how many lines in a file`
`$ cat `<filename>` | wc -l`

`# how many lines contains `<something>
`$ cat `<filename>` | grep -i `<something>` | wc -l`

`# how many lines contains `<something>` in all .txt files in a directory`
`$ cat *.txt | grep -i `<something>` | wc -l`

`# view first few lines of a file`
`$ head `<filename>
`$ cat `<filename>` | head`

`# view last few lines of a file`
`$ tail `<filename>

`# monitor changes in a file every 10 seconds`
`$ tail -f `<filename>` -n 10`

`# monitor changes in all .txt files in a directory every 10 seconds`
`$ tail -f *.txt -n 10`

### Convert line endings

`# windows to unix `
`$ dos2unix `<filename>

`# unix to windows`
`$ unix2dos `<filename>