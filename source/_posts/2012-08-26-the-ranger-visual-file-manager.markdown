---
layout: post
title: "The Ranger visual file manager"
date: 2012-08-26 17:10
comments: true
keywords: "ranger, file manager, config, zsh"
categories: tools
---

If you spend more than 2 hours with terminal everyday, like me. There is a tool you wish you could know earlier -- ranger.

{% img  /downloads/20120826_ranger.png [Ranger [Ranger File Manager zsh]] %}

<!--more-->

Very powerfull and very handy. Get the source from [here](http://www.nongnu.org/ranger/) and mannual in [here](http://www.nongnu.org/ranger/ranger.1.html).

Navigate use hjkl like vim and do what every finder can do with preview. (It can even preview photos)

If you are using zsh like me, to enable ranger in zsh, follow the steps below:

#### 1. In terminal:
{% codeblock lang:sh%}
    cat >> ~/.zshrc
{% endcodeblock %}
#### 2. Past the following code:
{% codeblock lang:sh%}
    #ranger file manager
    # source from, or add to ~/.zshrc
    # Ctrl-O opens zsh at the current location, and on exit, cd into ranger's last location.
    ranger () {
        command ranger "$(pwd)" <$TTY
        print -n "\033[A"
        zle && zle -I
        cd "$(grep \^\' ~/.ranger/bookmarks | cut -b3-)"
    }
    zle -N ranger
    bindkey "^O" ranger
{% endcodeblock %}
#### 3. Press Ctrl + D to end cat.

Then you are good to go!

--EOF--
