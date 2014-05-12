---
layout: post
title: "new file default permission and group"
date: 2014-05-09 01:18
comments: true
categories: linux
---

A new created file's owner will be the usr of current user id and in the group of current groupid in current session.

The fist group in the output of `groups` command is the primary group of current user.

    $ groups                                                                           
    ec2-user wheel

The primary group of a user can be set by `usermod -g wheel`.

`newgrp wheel` command can create a new shell with the changed group.

The default group for all files created in a particular directory can be fixed by setting the setgid flag on the directory (chmod g+s \<dir\>). New files in the directory will then be created with the group of the directory (set using chgrp \<group\> \<dir\>). This applies to any program that creates files in the directory.

Note that this is automagically inherited for new subdirectories (as of Linux 3.10), however, if sub-directories were already present, this change won't be applied to them (use the -R flag for that).


The new files default permission is controlled by `umask`.


### setuid(4), setgid(2) and sticky bit(1)

setuid, setgid on files allow anyone execute the file with the privilege of the owner/group, but many OS ignore setuid attribute due to security issues.

setgid on directories causes new files and subdirectoriesi created within it inherit it's group ID. setuid on directory is ignored on UNIX and Linux.

When setgid is set the permission shows: `drwxrwsrwx`, and if the folder don't have execution permission for the group, permission will be `drwxrwSrwx`.

The most common use of the sticky bit today is on directories. When the sticky bit is set, only the item's owner, the directory's owner, or root can rename or delete files. 

    $ ls -ld /tmp  
    drwxrwxrwt   4 root     sys          485 Nov 10 06:01 /tmp

If others don't have execution permission, it will be `drwxrwxrwT`.

To display the octal permissions:

    stat -c "%a %n" *


