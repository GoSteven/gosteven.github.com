---
layout: post
title: "Switching to ZSH"
date: 2012-05-10 21:31
comments: true
categories: shell
---
Following [Mako](http://en.wikipedia.org/wiki/Benjamin_Mako_Hill), after reading some posts regarding the benefit of using ZSH, finally I execute the command jumping to the zsh world:
    
    
    curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh
    
    
####The good thing####

It works pretty awesome. It "acts extremely similar to bash", but not always, which I will explain in the painful part. It does the typo correction which is very helpful to careless typers like me.  


####The pain during the switching####

After typing around with zsh, I was going to spreading it. I am using Octopress for blogging, I am astonished when I find out zsh shows the git folder status in the prompt. 

However, when I using rake to create a new post, it shows `zsh: no matches found: new_post[Switching to ZSH]`. I thought it was the ruby gem version problem as I installed something for OPENSHIFT of RedHat. But, it's not. 

The reason is zsh doesn't know about the RVM function, RVM need to be loaded into the shell session as a function. 

Append

    [[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"  # This loads RVM
    
to the .zshrc will fix the problem. 

####Investigate more####

Go through the [zsh user guide](http://zsh.sourceforge.net/Guide/), enjoy!
