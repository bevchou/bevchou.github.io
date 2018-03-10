---
layout: post
title: Lighting Controller Interface
date: 2018-03-07
type: post
categories:
- Tangible Interaction
tags:
- Interface
- DMX
- MKR1000
- Lighting
- Tangible Interaction
- Reed Switch
meta:
author:
   Beverly
---
![demo gif]({{ site.baseurl }}/assets/tangible-interaction/lightcontroldemo.gif)

For my lighting controller, I wanted to create an interface where someone would be able to map the position of the lights to the positions of actors (or anything) in the space. I used 6 reed switches that would correspond to the location of the 6 lights in the ITP lounge. Small game pieces with magnets on them were able to turn the lights on when placed over these locations on the controller.

I wanted to give more control than on/off, so I added the ability to change the brightness of all the lights that were on with a potentiometer. There is an LED to visually indicate the brightness in case there are no game pieces on the controller. I also included a toggle switch that will turn all the lights on/off at once.

<!--more-->

Here's a video of this working in the ITP lounge.

<p><div class="responsive-container"><iframe src="https://player.vimeo.com/video/259034258" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div></p>

To execute this concept, I needed to figure how to put the reed switches into a grid that would feel like the user's movement corresponds to the lights. I tested out {{ site.baseurl }}e spacing of the reed switches by feel, and where they would activate when under a piece of mat board. They have an oval shape area where they activate, so I tried to make a grid like this.


![reed sensor panel]({{ site.baseurl }}/assets/tangible-interaction/lightcontrol-reed-sensor-panels.jpg)

The switches are fragile since they're made of glass, so I hot glued them on the underside of mat board to keep them from bending while I soldered and organized the wires.

![wiring underneath]({{ site.baseurl }}/assets/tangible-interaction/lightcontrol-underside.jpg)

I also added a piece of mat board spaced off of the switches to protect them and provide a smooth surface.

![wiring inside]({{ site.baseurl }}/assets/tangible-interaction/lightcontrol-inside-wiring.jpg)

Here's a video of me testing the switches and printing out their states for the DMX channels I was trying to control.

<p><div class="responsive-container"><iframe src="https://player.vimeo.com/video/259033674" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div></p>

With the switches figured out, I needed to get the WiFi connection and DMX protocol working on the MKR1000. I based my code on Tom's sACN example and then added my code for my interface, replacing any "Serial.print()" commands with  "myController.setChannel(dmxChannel, value)". I also needed to add "myController.sendPacket(receiverAddress)" when I was ready to send my data to ITP's network. See the code below. I removed the IP address & wifi credentials from the code (;

<script src="https://gist.github.com/bevchou/8e2dd1a589825868548c8c4bf2340d85.js"></script>

The control worked pretty smoothly, but I think a good next step would be to experiment with using hall effect sensors instead of reed sensors. I think they might have a faster response to the magnets than the reed sensors and a more uniform (not oval shaped!) area where they can be activated. They also seem to be less fragile. I would also want to experiment with a logarithmic or linear potentiometer to see which is better to control light dimming.

![final with hands]({{ site.baseurl }}/assets/tangible-interaction/lightcontrol-final.jpg)

It's abstract and clean looking now, but a bit confusing. Visually, it would be better to have a way to slide in a map of the ITP lounge lights over the area with the reed switches. That way it was more clear to the user exactly which light they were turning on. Some labels for the knob and switch would be helpful as well.

![final no hands]({{ site.baseurl }}/assets/tangible-interaction/lightcontrol-final-no-hands.jpg)

Overall, I really enjoyed designing for the Tangible Interaction Workshop this semester. It's good to get more experience with p comp and to think through different used scenarios and data protocols! Thank you, Tom!
