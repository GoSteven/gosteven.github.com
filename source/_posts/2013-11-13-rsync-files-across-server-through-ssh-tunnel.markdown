---
layout: post
title: "rsync files across server through ssh tunnel"
date: 2013-11-13 00:56
comments: true
categories: 
---

The scenario is: I can ssh to Server A and Server B, but A and B cannot connect to each other. In order tot rsync file across server A and B, ssh tunnel is needed:
Firstly, set up reverse ssh tunnel to make it possible to ssh to local from Server A:
    ssh -R 1999:localhost:22 A_user@<A>
Then on Server A, create ssh tunnel to server B via local computer:
    ssh -f -N -L 2000:<B>:22 -p 1999 localuser@localhsot
The command above creates ssh tunnel in background, so you have to bother killing it after finishing rsyncing.
Finally, tell rsync to connect to localhost:2000 instead of <B>:22:
    rsync -rvP -e 'ssh -p 2000' dir/ B_user@<B>:/dir/
