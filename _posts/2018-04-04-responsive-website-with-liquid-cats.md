---
layout: post
title: Responsive Website with Liquid Cats
date: 2018-04-04
type: post
categories:
- Hacking the Browser
tags:
- HTML
- CSS
- Responsive
- Cats
- JQuery
meta:
author:
   Beverly
---
<div class="responsive-container"><iframe src="https://player.vimeo.com/video/264161984" width="640" height="400" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

There is a rule of physics that says cats are able to take the shape of any container. I'm proving that it's true, even in the browser. [CLICK HERE TO SEE FOR YOURSELF!!](http://itp.beverlychou.com/hacking-the-browser/w2-responsive-site/) Keep reading to see how I did it.

<!--more-->

I created a website that responds whenever someone resizes the window. To do this, I used the resize function in Jquery.

{% highlight ruby %}
$(window).resize(function() {
  //remove intro images - that was the gif and the text
  $('#start').remove();
  //pick images based on window width/height ratio
  let windowRatio = window.innerWidth / window.innerHeight;
  if (windowRatio >= 2) {
    newCat(WIDECAT.jpg);
  }
  //and then more if/then statements to select images
}

//function to change the cat image
function newCat(url) {
  $('#cat').attr('src', url);
}
{% endhighlight %}

From there it was a simple matter of determining which images I wanted to display. I tried to match the width/height ratio, width in pixels, and height in pixels to the images I used for the cats.

Here's the CSS I used on the cat images. The units 'vh' and 'vw' are units that are relative to the viewport. I had them both at 100 to fill the entire window. The object fit was used to make sure that the images maintained their original ratios, making sure the images didn't scale weirdly.

{% highlight ruby %}
#cat {
  position: fixed;
  top: 0;
  left:0;
  object-fit: cover;
  height: 100vh;
  width: 100vw;
}
{% endhighlight %}
