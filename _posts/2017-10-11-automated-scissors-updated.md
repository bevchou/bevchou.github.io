---
layout: post
title: Automated Scissors - Updated!
date: 2017-10-11 02:58:57.000000000 -04:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- P Comp
tags:
- Arduino
- NYU-ITP
- P Comp
- Servo
meta:
  _edit_last: '1'
author:
   Beverly
  
  
  
  
---
<p>Since this was a catch up week, I worked on fixing up my automated scissors project to reflect my original intent. This means I solved my problem of making my LED blink while the servo was in motion.</p>
<p>It turns out that using code for "blink without delay" solved my problem. However, it still took me an embarrassingly long time to figure out where to slide this piece of code into the rest of my Arduino sketch. I initially had it running outside of my loops to make the servo move and had it run when the "swtichState" variables were HIGH. I think this didn't work because the loop that moves the servo had to completed before doing anything else. I also tried using <a href="https://github.com/tigoe/Interval">Tom Igoe's Interval library</a>, which I couldn't make work for only the button press. Finally, I moved the blink without delay code into the right spot and my servo and blinking LED combination works! It needed to start right before the servo begins to move inside of the loop. Here it is working with the code below.</p>
<p><img class="alignnone size-full wp-image-285" src="{{ site.baseurl }}/assets/old-wp-content/updated-automated-scissors.gif" alt="" width="500" height="318" /><br />
<script src="https://gist.github.com/bevchou/94a9e576f4e5f91104c55bde911de1f1.js"></script></p>
<p><!--more--></p>
<p>Here is the full code for this project now. The circuit is still the same from my <a href="https://beverlychou.com/itp/2017/10/04/automated-scissors/">previous post</a>.</p>
<p><script src="https://gist.github.com/bevchou/f6946e82e4a9e77c80bc68e50025b138.js"></script></p>
