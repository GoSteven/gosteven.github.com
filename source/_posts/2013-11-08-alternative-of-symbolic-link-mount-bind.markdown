---
layout: post
title: "Alternative of symbolic link : mount --bind"
date: 2013-11-08 06:36
comments: true
categories: 
---

Symbolic link works well in most cases, but it differs from the "real" file path. For example, symb link could be disabled by nginx. Hard link has it's own limitations like you cannot hard link directory.

The alternative is using:

    $ sudo mount --bind /source_path /dest_path

What is does is:
>Remount a subtree somewhere else (so that its contents are available in both places)

The only thing to keep in mind is that you can't `rm -rf` the dest folder, you have to unmount it first.
