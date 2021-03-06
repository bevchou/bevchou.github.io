---
layout: post
title: Automated Scissors
date: 2017-10-04 04:04:47.000000000 -04:00
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
  _oembed_768df976a013978205a5333f3389588c: "{{unknown}}"
  _oembed_1d65e839c8dfa8967d8077ee4ce3195b: "{{unknown}}"
author:
   Beverly
  
  
  
  
---
<p>To follow up on my previous issue with LED blinking... I decided instead of flashing, the LED should stay on to indicate when the servo is moving. I did explore a few methods for blink without delay using millis(), but I had trouble making it only blink when the button was pressed and only for the duration of the servo's motion. Anyways, I automated a pair of scissors using a servo. It runs at two speeds depending on how fast you want to cut some paper. Here is a gif of it in action.</p>
<p><img class="alignnone wp-image-248" src="{{ site.baseurl }}/assets/old-wp-content/automated-scissors-vid.gif" width="600" height="370" /></p>
<p><!--more--></p>
<p>Here is the circuit diagram. Following my previous post, I was confident that all the parts were wired up correctly.</p>
<p><img class="alignnone " src="{{ site.baseurl }}/assets/old-wp-content/automated-scissors-circuit-diagram.jpg" width="290" height="425" /></p>
<p>And here is my final code.</p>
<p><script src="https://gist.github.com/bevchou/6087e1ee41294c852a7a90a2d3032e68.js"></script></p>
<p>Next, I made a box to mount my scissors to. After measuring all my pieces, I intended for it to look like this with all the components inside. The box is 3" tall to fit the components and the full motion of the scissors, which isn't shown in the drawing.</p>
<p><img class="alignnone " src="{{ site.baseurl }}/assets/old-wp-content/box-dimensions.jpg" width="353" height="249" /></p>
<p><img class="alignnone " src="{{ site.baseurl }}/assets/old-wp-content/internal-components-stack-up.jpg" width="350" height="390" /></p>
<p>I used cardboard from the recycling bin, and the build up of the box was fine. But... I was unable to get the LED and buttons to line up very well with the hole I cut out in the top. The cardboard was too thick, so the buttons couldn't be pressed easily. I decided to put my electronic parts on top, and run my power cord through the hole. I also used copious amounts of tape to anchor my servo. The scissors are secured with a zip tie that is in two slots to accommodate the scissor's movement when the servo is rotating. It's not beautiful, but it works for this prototype. The first image is the outside of the box, and the second image is the inside of the box.</p>
<p><img class="alignnone " src="{{ site.baseurl }}/assets/old-wp-content/automated-scissors.jpg" width="450" height="292" /></p>
<p><img class="alignnone " src="{{ site.baseurl }}/assets/old-wp-content/inside-of-box.jpg" width="450" height="275" /></p>
<p>If I was going to make a more polished version of this device, I would create a plastic enclosure that would allow my breadboard and Arduino to mount securely. I'd need to wire the buttons and LED to the top of the enclosure, and use different fasteners to secure the servo.</p>
