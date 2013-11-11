---
layout: post
title: "SSH ControlMaster"
date: 2013-11-11 03:40
comments: true
categories: 
---

Lots of people recommond using ControlMaster:

    Host *
    ControlMaster auto
    ControlPath /tmp/%r@%h:%p

This will re-use the exiting connections instead of creating a new one, so that it can speed up the ssh connection.

To make it more convenient, this line can be added to `~/.ssh/config`

    ControlPersist 600

This will make the ControlMaster stay alive for 600 seconds after last existing ssh session is quit.

A regular issue I encountered using ControlMaster is that in some cases I want to kill ssh ControlMaster active connection.

For example, when I run ssh tunnel command `ssh -L 8888:localhost:8888 host.com` twice, the tunnel won't work anymore. 

In order to kill the active connection, use 

    ssh -O check host.com

to check status, and 

    ssh -O exit host.com

to exist the active connection.

If you want to delete all connections (not just the connection to a particular host) in one fell swoop, then `fuser /tmp/ssh_mux_*` or `lsof /tmp/ssh_mux_*` will list the ssh clients that are controlling each socket. Use `fuser -HUP -k tmp/ssh_mux_*` to kill them all cleanly (using SIGHUP as the signal is best as it lets the clients properly remove their socket).

