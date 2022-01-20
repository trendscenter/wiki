---
layout: default
title: VNC
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

## Create a VNC starter file on the cluster

Log in to the cluster head node or a dev node and do the following:

```
# login to the dev node 
ssh -XY devtrendsgpu

# create ~/.vnc
mkdir ~/.vnc
cd ~/.vnc

# create a xstartup file
vi xstartup
```

Edit the contents of the `xstartup` like below:

```
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
# /etc/X11/xinit/xinitrc
# vncserver -kill $DISPLAY
xrdb $HOME/.Xresources
xfce4-session &
```

To save the content and exit out of `vim`, do `Ctrl+C` followed by `:wq` then enter.

## Start VNC server on the cluster

Login to a dev node and start the VNC server. 
It will help a lot if you set up the SSH config as described in [Configure SSH for easy access to DEV machines](Configure_SSH_for_easy_access_to_DEV_machines), including the forwarding/tunneling part.

```
host devtrendsgpu
    HostName trendsagn019.rs.gsu.edu
    user <campusID>
    LocalForward <port> localhost:<port>
```

Note on port selection: the port used for each instance of every application needs to be unique. 
To make sure you are using a unique port and not blocking someone else, it is suggested that you prefix the port number with your cubicle/office number.
For example, if your office number is 18201, use 18201 for Jupuyter, 18202 for VNC, and so on.  

```
# login to the dev node 
ssh -XY devtrendsgpu

# start VNC server
vncserver -rfbport <port>
```

## Connect to the VNC server from local machine

Install a VNC client application on your local machine, e.g. [tightvnc](https://www.tightvnc.com/download.php), [tigervnc](https://sourceforge.net/projects/tigervnc/) or [vncviewer](https://www.realvnc.com/en/connect/download/viewer/).
Then use `localhost:<port>` as the address to connect to the VNC session started above.



