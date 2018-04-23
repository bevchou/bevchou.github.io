---
layout: post
title: Endless Scroll Bookmarklet
date: 2018-04-12
type: post
categories:
- Hacking the Browser
tags:
- HTML
- CSS
- Bookmarklet
- Javascript
meta:
author:
   Beverly
---
![bookmarklet gif]({{ site.baseurl }}/assets/hackbrowser/w3-bookmarklet-gif.gif)

I'm pretty sure at some point we've all had the following thought - "Wow, if only I could spend even more of my life scrolling." Now you can!!! <a href="javascript:!function(){function%20e(){size+=1,sizeTxt=size+%22px%22,i()}function%20i(){document.body.style.paddingTop=sizeTxt}setInterval(e,10),size=0,sizeTxt}();">DRAG THIS LINK INTO YOUR BOOKMARKS FOR ENDLESS SCROLLING FUN!</a>

<!--more-->

This was a simple little bookmarklet. I used the setInterval function to call a function that increases the padding in set intervals. It

{% highlight ruby %}
//this will run the callback function every t milliseconds
interval = setInterval(callbackToIncrementPadding, t);
{% endhighlight %}



And then inside my callback, I call a function that actually send that info to the browser.

{% highlight ruby %}
function setSize() {
  document.body.style.paddingTop = sizeTxt;
}
{% endhighlight %}

Finally, I used the [Bookmarkleter](http://chriszarate.github.io/bookmarkleter/) to convert my javascript into a bookmarklet.
