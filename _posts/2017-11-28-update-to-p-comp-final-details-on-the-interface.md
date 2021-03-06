---
layout: post
title: Update to P Comp Final - Details on the interface
date: 2017-11-28 21:47:17.000000000 -05:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- P Comp
tags:
- Ableton
- Arduino
- Final
- Interface
- Music
- NYU-ITP
- P Comp
- Prototype
meta:
  _edit_last: '1'
author:
   Beverly




---
<p>Since the last class, Brandon and I have run a quick prototype of our project and created another design/prototype for the music interface.</p>
<p><!--more--></p>
<p>For the prototype, the Arduino was connected to Ableton to control the sounds and effects. The LEDs were set up to light up in the random glitter pattern whenever the user hit a button on the interface. We want to make the mapping for the lights and sound more connected than just random, which is something we will work on moving forward. This is what the breadboard version looked like for our user testing.</p>
<p><img class="alignnone size-full wp-image-427" src="{{ site.baseurl }}/assets/old-wp-content/breadboard-prototype-interface.jpg" alt="" width="337" height="350" /></p>
<p>And this is what some user testing looked like (thanks to Carrie, Haiyi, and Simon).</p>
<p><iframe src="https://player.vimeo.com/video/244939932" width="331" height="500" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p><img class="alignnone size-full wp-image-430" src="{{ site.baseurl }}/assets/old-wp-content/under-the-table-prototype-on-the-outside.jpg" alt="" width="653" height="400" /></p>
<p><img class="alignnone size-full wp-image-428" src="{{ site.baseurl }}/assets/old-wp-content/prototype-under-table-testing.jpg" alt="" width="533" height="400" /></p>
<p>We got some of the following feedback from our users:</p>
<ul>
<li>Good with 2 people - forces you to connect with them</li>
<li>Fun to play with</li>
<li>Crawling under the table is reminds user of being a kid</li>
<li>Controlling the other person's sound with your knob would be a fun interaction</li>
<li>Want to look at lights behind the person you’re in the tent with. That makes you look up and interact with the person you’re with</li>
<li>Make it a pillow fort</li>
</ul>
<p>Some observations by me:</p>
<ul>
<li>One user tried to play songs (happy birthday was the song of choice) that they knew from playing the piano. She was able to do so since the buttons had the notes in order.</li>
<li>People were happy to crawl under a table with a sheet draped around it.</li>
<li>Users did not know the lights were random, but still I think more variation would keep users engaged.</li>
</ul>
<p>Using some of this feedback, I designed a interface for the instrument part of our project. The circles are the buttons that play melodic sounds. These are basically akin to playing piano keys. The dials (circles with the line on it) are ways to control sound effect. The squares with the patterns in the middle of the interface art capacitive touch panels where people can play percussion sounds by tapping and hitting them with their fingers. I though that tapping with your finger had a more immediate feedback that is fitting for percussion.</p>
<p><img class="alignnone wp-image-431" src="{{ site.baseurl }}/assets/old-wp-content/interface-drawing.jpg" alt="" width="497" height="260" /></p>
<p>And after buying some parts for Adafruit, I made a cardboard interface. I used this to get a feel for how I wanted the spacing of the components to be to fit people's hands. I have the buttons on the right side since I am assuming that you would play the melodic stuff with your right hand (like a piano player) and control the knobs with your left hand.</p>
<p><img class="alignnone size-full wp-image-433" src="{{ site.baseurl }}/assets/old-wp-content/cardboard-prototype-for-music-interface.jpg" alt="" /></p>
<p>I got some feedback from Tom before Thanksgiving, and here are some things that we are thinking about.</p>
<ul class="ul1">
<li class="li1">It might be better to keep the sounds constant to give users constraints. This would make them play music instead of flipping through options.</li>
<li class="li1">Definitely think about how the sound is connected to the lights. Need to move beyond the random glitter function.</li>
<li class="li1">Possibly use a midi synth (see what the ER has) instead of Ableton on a laptop. This could simplify things and provide better sound.</li>
</ul>
