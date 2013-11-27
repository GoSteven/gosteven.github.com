---
layout: post
title: "Find missing number in a random ordered list"
date: 2013-11-25 22:15
comments: true
categories: 
---

Imagine you have a list of all the numbers from 1 to n in a list, except one of the numbers is missing, (therefore the list has (n-1) numbers), and the numbers are in a random order in the list.How do you find out which number is missing?

  
<pre>
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
</pre>

Answer:

    sum(xrange(1, n+1)) - sum(list)
P.S. Even better: 
    n * (1 + n) / 2 - sum(list)
