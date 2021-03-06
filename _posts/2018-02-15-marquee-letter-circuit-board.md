---
layout: post
title: Marquee Letter Circuit Board
date: 2018-02-15 15:13:21.000000000 -05:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Homemade Hardware
tags:
- ATtiny85
- Eagle
- NYU-ITP
- Othermill
- Soldering
meta:
  _edit_last: '1'
author:
   Beverly




---
<p><img class="alignnone size-full wp-image-596" src="{{ site.baseurl }}/assets/old-wp-content/working-circuits.gif" alt="" /></p>
<p>My marquee letter works! Keep reading below.</p>
<!--more-->
<p>My Eagle files worked out well and I was able to make sure my circuit had no fly wires. I did originally think that components would be interchangeable when laying out the board for my letter (so all resistors the same &amp; all LEDs the same), but this was not the case. I ended up needing to redo my layout a few times to get the resistors and LEDs in sequential order.</p>
<p><img class="alignnone wp-image-592" src="{{ site.baseurl }}/assets/old-wp-content/LED-Letter-Board-Schematic-Screenshot.png" alt="" width="596" height="133" /> <img class="alignnone wp-image-593" src="{{ site.baseurl }}/assets/old-wp-content/LED-Letter-Board-Layout-Screenshot.png" alt=""  /></p>
<p>After spending some time at the Othermill, breaking a bit, and soldering for hours....</p>
<p><img class="alignnone size-full wp-image-590" src="{{ site.baseurl }}/assets/old-wp-content/back-of-letter.jpg" alt=""  /></p>
<p><img class="alignnone size-full wp-image-587" src="{{ site.baseurl }}/assets/old-wp-content/front-of-letter-lights-on.jpg" alt="" /></p>
<p>Yay! There was a resistor that wasn't fully soldered, which is why one LED is off, but I fixed it. And for my ATtiny85 board, I was able to get things pretty compact. I wished there was a way to dimension the holes, but I ended up kind of placing them by eye since I couldn't find a tool to do it more precisely.</p>
<p><img class="alignnone wp-image-594" src="{{ site.baseurl }}/assets/old-wp-content/ATtiny85-Schematic-Screenshot.png" alt="" width="543" height="319" /> <img class="alignnone wp-image-595" src="{{ site.baseurl }}/assets/old-wp-content/ATtiny85-Board-Layout-Screenshot.png" alt=""  /></p>
<p>And then I had some issues with this one at the Othermill. Some of the holes were too small so they didn't get drilled. I had to redo it making sure that the holes were properly sized in Eagle.</p>
<p><img class="alignnone size-full wp-image-591" src="{{ site.baseurl }}/assets/old-wp-content/back-of-ATtiny85-circuit.jpg" alt=""  /></p>
<p><img class="alignnone size-full wp-image-589" src="{{ site.baseurl }}/assets/old-wp-content/front-of-ATtiny85-circuit.jpg" alt=""/></p>
<p>I noticed that the black boards cut a little more cleanly than the yellow boards. I wish I had added a hole to panel mount my switch, but instead it is kind of floating off the board.</p>
