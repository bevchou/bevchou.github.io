---
layout: post
title: ICM Week 7 - Extra!
date: 2017-10-24 02:11:35.000000000 -04:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- ICM
tags:
- DOM
- Giphy API
- ICM
- NYU-ITP
- p5.js
meta:
  _edit_last: '1'
author:
   Beverly




---
<p>So, now I've updated my gif slider to take inputs from the user. <a href="https://beverlychou.com/ICM/W7-p5-general-gif-slider-giphy-api/">Click here to play with it! </a></p>
<p><img class="alignnone size-full wp-image-352" src="{{ site.baseurl }}/assets/old-wp-content/Screen-Shot-2017-10-24-at-3.00.16-AM.png" alt="" /></p>
<p>Some nice inputs that have output gifs that make some sense are things like happy/sad or hello/goodbye. Obviously you can get a lot of weird gifs if you want, but I've got it set for a PG rating (:</p>
<p><!--more--></p>
<p>Essentially, I altered the code to take user inputs from the DOM. Here is the HTML file below.</p>
<p><script src="https://gist.github.com/bevchou/4377fb26dd907f4a79b13058480e49bc.js"></script></p>
<p>And then this is the p5.js file below. Essentially, I selected in the inputs from the left and right fields and then input their values into my Giphy API query url. I had to move the <span class="pl-en">loadJSON</span>() file into the function updateGif() so that it would reload the new JSON files each time the user pressed the "Go!" button. Pretty much everything else is the same as in my previous post though!</p>
<p><script src="https://gist.github.com/bevchou/17716043ace42792276bda4c1d87b951.js"></script></p>
