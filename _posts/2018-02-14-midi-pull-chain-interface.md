---
layout: post
title: MIDI Pull Chain Interface
date: 2018-02-14 02:26:19.000000000 -05:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Tangible Interaction
tags:
- Arduino
- GarageBand
- MIDI
- NYU-ITP
- Pull Switch
- Tangible Interaction
meta:
  _edit_last: '1'
  enclosure: "https://beverlychou.com/itp/wp-content/uploads/2018/02/for-blog.mov\r\n51809431\r\nvideo/quicktime\r\n"
author:
   Beverly




---

<div class="responsive-container"><iframe src="https://player.vimeo.com/video/259807241" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

<p>For the MIDI interface, Anthony and I worked together to make a MIDI pull chain interface that is combined with effects controls. We were both excited to use pull chains! Essentially, you can build chords by turn notes on and off with the pull chain switches. The notes will sustain until you turn them off &amp; you can tell if they are on/off when the corresponding LEDs are on/off.</p>

<p><img src="{{ site.baseurl }}/assets/old-wp-content/Photo-Feb-13-11-59-58-PM.jpg" alt=""  /></p>

We also made interfaces to control different effects. We have a sliding switch with springs back to the center that does pitch bending. The drum pad that has a piezo sensor under a piece of silicone changes note velocity.

<p><img src="{{ site.baseurl }}/assets/old-wp-content/Photo-Feb-14-1-42-22-AM.jpg" alt=""  /></p>

<p><!--more--></p>

<p>To get all these components working together we had the MIDI-to-USB box hooked up to two Arduino circuits. Yes, we are sending MIDI protocol to one play instrument using two Arduinos! Then we hooked up the USB to GarageBand on a computer to play some sounds.</p>
<p><img src="{{ site.baseurl }}/assets/old-wp-content/Photo-Feb-13-7-25-42-PM.jpg" alt=""  /></p>
<p>Here is the code for the pull chain part:</p>
<p><script src="https://gist.github.com/bevchou/1b9b7168153bb2c79ac450cf071340b9.js"></script></p>
<p>And here is a link to the code for the effects controllers <a href="https://github.com/79/tangible-midi-test/blob/master/tangible-midi-test.ino">here</a>.</p>
<p>We need to refine a few things, but overall it works. We based a lot of our code on the examples from the <a href="https://itp.nyu.edu/physcomp/labs/labs-serial-communication/lab-midi-output-using-an-arduino/">P Comp MIDI example</a> as well as <a href="https://github.com/tigoe/ArduinoGeneralExamples/blob/master/M0MidiController/M0MidiController.ino">Tom's code from class</a>. The Arduino Unos did not have two serial ports, so we needed to control MIDI through software serial.</p>
<p>The build concept was not that complicated, but the wiring was a bit messy.</p>
<p><img  src="{{ site.baseurl }}/assets/old-wp-content/Photo-Feb-13-3-34-07-PM.jpg" alt=""  /></p>
<p><img  src="{{ site.baseurl }}/assets/old-wp-content/Photo-Feb-13-11-59-50-PM-1.jpg" alt=""  /></p>

<p><div class="responsive-container"><iframe src="https://player.vimeo.com/video/257324319" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div></p>
