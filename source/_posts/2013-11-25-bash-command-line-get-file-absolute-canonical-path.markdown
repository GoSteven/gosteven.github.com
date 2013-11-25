---
layout: post
title: "bash command line get file absolute(canonical) path"
date: 2013-11-25 00:08
comments: true
categories: 
---

To print absolute path to a file:

    $ readlink -m <file>

or use python script:

    import sys
    import os
    for path in sys.argv[1:]:
        print os.path.realpath(path)

or use bash:

    echo $(cd $(dirname $1); pwd)/$(basename $1)
