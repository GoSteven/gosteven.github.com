---
layout: post
title: "Multiple sliders on one page - jquery"
date: 2012-08-29 21:52
comments: true
keywords: "slider, jquery, multiple on one page"
categories: jquery
---

I was trying to put several sliders on the same page. There are actually lots of tutorials can tell you how to do that, like [this one](http://demo.tutorialzine.com/2011/12/what-you-need-to-know-html5-range-input/slider-jqueryui.html).

However, I want multiple, like this:

{% img  /downloads/20120829_slider.png [Slider [Multiple slider on one page]] %}

<!--more-->

In the sample code, the javascript looks like this:

{% codeblock lang:js%}
$(function(){
    var currentValue = $('#currentValue');
    $("#slider").slider({ 
        max: 500,
        min: 0,
        slide: function(event, ui) {
            currentValue.html(ui.value);
        }
    });
});
{% endcodeblock %}

They find the html element by id. But when I generate sliders in a loop, it would be nasty to assign ids to each slider:

{% codeblock lang:html%}
{% raw %}
<div id="search_bar">
    {% for pp in p %}
    <div class="contSlider">
         <h4>{{ pp.field_name }}</h4>
         <div class="slider"></div>
         <p class="note">Current value: <span class="currentValue">0</span></p>
    </div>
    {% endfor %}
</div>
{% endraw %}
{% endcodeblock %}

Fortunately  `each()` in jquery is very handy, we can get all the divs, and loop through them:

{% codeblock lang:js%}
$(function(){
    $('.contSlider').each(function(i,obj) {
        var currentValue = $(obj).find('.currentValue')
        var slider = $(obj).find('.slider')
        slider.slider({
            max: 500,
            min: 0,
            slide: function(event, ui) {
                currentValue.html(ui.value);
            }
        });
    });
            
});
{% endcodeblock %}

When using `each()` sometime you could encounter error like: 
>  "Uncaught TypeError: Object #<HTMLDivElement> has no method 'find'"

This is because the `obj` in `$('.contSlider').each(function(i,obj) {` refers to a DOM object rather than a jquery object.

Add `$()` to make it a jquery object like this: `$(obj).find('.currentValue')`.

In the end, what I got is:

<link rel="stylesheet" href="http://ajax.googleapis.com/ajax/libs/jqueryui/1.8.16/themes/base/jquery-ui.css" />
<div class="contSlider">
     <h4>slider 1</h4>
     <div class="slider"></div>
     <p class="note">Current value: <span class="currentValue">0</span></p>
</div>
<div class="contSlider">
     <h4>slider 2</h4>
     <div class="slider"></div>
     <p class="note">Current value: <span class="currentValue">0</span></p>
</div>
<script src="http://code.jquery.com/jquery-1.7.1.min.js"></script>
<script src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.16/jquery-ui.min.js"></script>
<script >
    $(function(){
        $('.contSlider').each(function(i,obj) {
            var currentValue = $(obj).find('.currentValue')
            var slider = $(obj).find('.slider')
            slider.slider({
                max: 500,
                min: 0,
                slide: function(event, ui) {
                    currentValue.html(ui.value);
                }
            });
        });
    });
</script>


--EOF--


