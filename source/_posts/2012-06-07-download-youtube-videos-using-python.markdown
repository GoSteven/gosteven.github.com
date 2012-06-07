---
layout: post
title: "Download YouTube videos using python"
date: 2012-06-07 13:17
comments: true
categories: python
description: "Download YouTube video using python"
keywords: "python, download youtube, youtube download, download youtube video"
---

I have searched around to find a simple way to download youtube video. However, google hasn’t provide an API for downloading, and youtube page content structure seems has changed a lot, some old post regarding how to download youtube video in [one line python script](http://abhinay.wordpress.com/2010/05/12/downloading-youtube-videos-using-python-one-liner/) doesn’t work any more.


Finally I find an actively repository on github and forked it: [python-youtube-download](https://github.com/GoSteven/python-youtube-download).  To make it simpler to use rather than selecting the definition and specifying the format, I added main script to enable it to run in one line:
    
    python youtube.py "http://www.youtube.com/watch?v=6bXOOz8mN6U"

