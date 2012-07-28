---
layout: post
title: "Vertically scale web application via using non-blocking I/O"
date: 2012-07-28 21:51
comments: true
categories: technique
keywords: " vertically scale, non-blocking IO, web"
---

I have been working on web application scaling for a while. There are lots of interesting stuff. I will scale vertically first.

Non-blocking I/O
----

Blocking I/O means that the program execution is put on hold while the I/O is going on, which means the program waits until the I/O is finished and then continues it's execution. 

However, in non-blocking I/O, the program can continue during I/O operations, and is notified via a callback when IO operation is finished. This forces programmers to design programs differently making them perform a lot better.

The Non-blocking I/O was supported by most Operation Systems. On Windows there is underlying OS support for non-blocking I/O, and Microsoft's CLR(Common Language Runtime, virtual machine component of .NET framework) takes advantage of that.


Non-blocking I/O for web applications
----

The implementation of non-blocking IO contribute the success of projects like [node.js](http://nodejs.org/).

For common web applications like JAVA Servlet, Apache web server , there is a design flaw, which introduce lots of overheads consume lots of mem and cpu because the thread is expensive. Non-blocking I/O is smart as the pending I/O connections will not consume any resources. On the other hand, underlying OS will be exhausted when looping through threads and checking status if each request will be handled via threads. 

Here is a good slide describe node.js:
<iframe src="http://www.slideshare.net/slideshow/embed_code/2693037" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="http://www.slideshare.net/marcusf/nonblocking-io-event-loops-and-nodejs" title="Non-blocking I/O, Event loops and node.js" target="_blank">Non-blocking I/O, Event loops and node.js</a> </strong> from <strong><a href="http://www.slideshare.net/marcusf" target="_blank">Marcus Frödin</a></strong> </div>

