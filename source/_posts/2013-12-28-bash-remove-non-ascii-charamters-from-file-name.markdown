---
layout: post
title: "bash remove non-ascii charamters from file name"
date: 2013-12-28 03:04
comments: true
categories: 
---

    ls -1 | while read file; do N=$(echo $file | tr -cd '\11\12\40-\176'); mv "$file" "$N"; done

What this does is:

* list filename in the current directory 
* -c means complement -d delete
