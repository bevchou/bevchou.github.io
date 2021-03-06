---
layout: post
title: Working with Servo Motors
date: 2017-10-03 02:22:58.000000000 -04:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- P Comp
tags:
- Arduino
- ITP-NYU
- LED
- P Comp
- Servo
meta:
  _edit_last: '1'
  _oembed_5b670dcf06776c965f4727761e467fba: "{{unknown}}"
author:
   Beverly




---
<p>I am currently working on this week's project for Physical Computing and I am running into some issues with servo motors. Specifically, how I can do other things while the servo motor is running.</p>
<p>First, I'll go over what I've done so far to check that certain parts of my circuit and code are definitely working. I started by making a circuit to control the servo using a potentiometer. Before putting in a servo, I used an LED to make sure I wired the potentiometer correctly.</p>
<p><img class="alignnone wp-image-248" src="{{ site.baseurl }}/assets/old-wp-content/LED-potentiometer-circuit-smallerfile.gif" alt="" width="355" height="414" /></p>
<p>Next, I swapped out the LED for my servo and updated my code to use the servo library.</p>
<p><img class="alignnone wp-image-250" src="{{ site.baseurl }}/assets/old-wp-content/servo-pot-circuit-diagram.jpg" alt="" width="354" height="216" /><br />
<img class="alignnone wp-image-251" src="{{ site.baseurl }}/assets/old-wp-content/servo-pot-circuit-smallerfile.gif" alt="" width="450" height="305" /><br />
<script src="https://gist.github.com/bevchou/1b8d92861187a6f2c58ebc6160330f91.js"></script></p>
<p>All of this was working great. So I know for this week's project I want to have a servo that will go through its motion and then return to the original position after it completes its travel. I am able to get this working as shown below.</p>
<p><img class="alignnone wp-image-251" src="{{ site.baseurl }}/assets/old-wp-content/scissor-servo-without-led-blink-smallerfile.gif" alt="" width="450" height="321" /></p>
<p>And then because I will have an option (via push buttons) to choose a slow or fast speed, I want the LED to blink either fast or slow accordingly. I added the LED blinking code using delays, but it slows down my servo's motion to a crawl.</p>
<p><img class="alignnone wp-image-251" src="{{ site.baseurl }}/assets/old-wp-content/servo-with-led-blink-moving-hella-slow-smallerfile.gif" alt="" width="450" height="314" /><br />
<script src="https://gist.github.com/bevchou/5642bd62908db30b10f20e5837289bb4.js"></script></p>
<p>I know it's going through the delays each time it loops to move my servo, so I am looking into ways to avoid using delays to get my LED to blink. Or is it only possible stop the slowing down by running one output at a time? I doubt it, so I'm going to keep looking into solutions.</p>
