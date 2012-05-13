---
layout: post
title: "Concurrent tasks execution in Python"
date: 2012-05-13 13:37
comments: true
categories: 
---
There are tasks need to be done with multiple thread, e.g.: I need to request thousands of urls, in order to training the collaborative filtering service. This could easily be done using python.

###First way: Manage the thread yourself
I have a repo on Github, [Tumblr Image Downloader](https://github.com/GoSteven/tumblrimgdownloader/blob/master/imgdl.py), which is used for batch download images from a tumblr blog using tumblr API.

Basically, there is a *task queue*:

    q = Queue()
 
and a *worker*:

    def worker():
        while True:
            download_img(q.get(), save_path)
            q.task_done()

What the *download_img* function does is get the image url and save it to the *save_path*. 
            
The program will call the *download_imgs* function:
    
    def download_imgs(imgs_src, save_path, num_workers):
        for i in range(num_workers):
            t = Thread(target=worker)
            t.setDaemon(True)
            t.start()
        for img_src in imgs_src:
            q.put(img_src, save_path)
        q.join()
        
    download_imgs(imgs_src, save_path, numthreads)
    
###Better and Simpler way: Using concurrent.futures module
[PEP 3148](http://www.python.org/dev/peps/pep-3148/) gives the motivation for this module:
>Python currently has powerful primitives to construct multi-threaded and multi-process applications but parallelizing simple operations requires a lot of work i.e. explicitly launching processes/threads, constructing a work/results queue, and waiting for completion or some other termination condition (e.g. failure, timeout). It is also difficult to design an application with a global process/thread limit when each component invents its own parallel execution strategy.

This module will make the life easier. Download link is [here](http://pypi.python.org/pypi/futures). There are two types of executor: ThreadPoolExecutor and ProcessPoolExecutor.

I will take ThreadPoolExecutor for example:

    import concurrent.futures
    import urllib.request

    URLS = ['http://www.foxnews.com/',
            'http://www.cnn.com/',
            'http://europe.wsj.com/',
            'http://www.bbc.co.uk/',
            'http://some-made-up-domain.com/']

    def load_url(url, timeout):
        return urllib.request.urlopen(url, timeout=timeout).read()

    with concurrent.futures.ThreadPoolExecutor(max_workers=5) as executor:
        future_to_url = dict((executor.submit(load_url, url, 60), url)
                             for url in URLS)

        for future in concurrent.futures.as_completed(future_to_url):
            url = future_to_url[future]
            if future.exception() is not None:
                print('%r generated an exception: %s' % (url,
                                                         future.exception()))
            else:
                print('%r page is %d bytes' % (url, len(future.result())))
        
-EOF-
