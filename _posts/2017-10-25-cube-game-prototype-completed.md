---
layout: post
title: Cube Game Prototype Completed!
date: 2017-10-25 01:50:25.000000000 -04:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- P Comp
tags:
- Arduino
- Game
- Midterm
- NYU-ITP
- P Comp
meta:
  _edit_last: '1'
author:
   Beverly
  
  
  
  
---
<p><iframe src="https://player.vimeo.com/video/239765530" width="640" height="360" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>We finished our prototype! We still need to do some final clean up, but here's a video of us getting it to work in the enclosure for the first time.</p>
<p>Read more below and also at<a href="http://www.chattinoutloud.com/2017/10/25/pcomp-midterm-cube-switch-game/"> Marco's blog post</a>!</p>
<p><!--more--></p>
<p>On Monday and Tuesday this week, we worked on fabricating our box. Marco picked out <a href="http://a.co/bqvXfFr">these arcade buttons</a> and some 1/4" acrylic which fit with the game theme of the box. I started by using the <a href="https://makeabox.io/">makeabox.io </a>site to get the general plan for the box, and then I altered it to include holes for the buttons and a lid at the top. A screenshot of the Illustrator file is below.</p>
<p><img class="wp-image-358 alignnone" src="{{ site.baseurl }}/assets/old-wp-content/laser-cutter-ai-file.png" alt="" width="529" height="283" /></p>
<p>Here is the laser cutter in action!</p>
<p><img class="alignnone size-full wp-image-360" src="{{ site.baseurl }}/assets/old-wp-content/laser-cutter-in-progress.jpg" alt="" width="543" height="350" /></p>
<p>I wish we used the 75 Watt Epilog laser cutter instead of the 60 Watt Epilog since it took approximately 10 passes for the laser to cut through the 1/4" acrylic. We chatted with some shop staff, and this could be due to laser cutter being run constantly all day without being reset or maintained. We used the laser cutter at the end of the night so this is a definite possibility. Alternately, we could've gone with a thinner acrylic. It all worked out in the end, and then we needed to build the box and reassemble our Arduino circuit to go inside our enclosure. We used some plastic glue to assemble our box.</p>
<p><img class="alignnone size-full wp-image-359" src="{{ site.baseurl }}/assets/old-wp-content/box-progress-on-floor.jpg" alt="" width="350" height="347" /></p>
<p>And then we added the buttons. These were nice because they just press fit into the holes we cut out.</p>
<p><img class="alignnone size-full wp-image-364" src="{{ site.baseurl }}/assets/old-wp-content/box-assembly-3.jpg" alt="" width="313" height="350" /></p>
<p>Finally, we rebuilt our circuit to hook up to the arcade buttons and LEDs. As you can see, the LEDs are secured with tape. We added an on/off switch, but this only turns off the buttons, which are powered through the breadboard, not the LEDs, which are still powered by the Arduino digital output pins. To get the switch to function properly, I think we need to wire the Arduino's incoming power in series with the on/off switch. This wasn't really possible since our box is wired to a computer to connect with the p5 sketch (and for power). We tried to use battery power and a Bluetooth connection to make it wireless, but we couldn't figure out the Bluetooth chips from the shop. They are the newer version low energy ones, which I am not sure are compatible with the serial connection we have been using. As a result our box is wired, though unfortunately we did not want it to be. This is something we would want to fix in a future iteration of this project.</p>
<p><img class="alignnone size-full wp-image-363" src="{{ site.baseurl }}/assets/old-wp-content/wiring-box.jpg" alt="" width="350" height="496" /></p>
<p><img class="alignnone size-full wp-image-362" src="{{ site.baseurl }}/assets/old-wp-content/inside-box.jpg" alt="" width="350" height="478" /></p>
<p>Finally, we closed up the lid &amp; played the game as shown in the video at the top. More thoughts on the interaction and better videos/images will be in an updated post!</p>
