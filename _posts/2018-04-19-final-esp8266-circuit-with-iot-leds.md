---
layout: post
title: Final ESP8266 Circuit with IoT LEDs
date: 2018-04-19
type: post
categories:
- Homemade Hardware
tags:
- ESP8266
- Othermill
- Neopixels
- SMD Parts
- Eagle
meta:
author:
   Beverly
---
![picture of final circuit]({{ site.baseurl }}/assets/homemadehardware/final-the-finalresult.jpg)

The process of taking my breadboard circuit to SMB part circuit was such a struggle omg. Here is the board I ended up with, which looks really nice, but unfortunately does not work. Code appears to upload through the Arduino IDE, but there is some issue with the board stuck in a reset loop.

Even though my circuit doesn't work, the code does work!!! It works 100% on my breadboard circuit and the Feather Huzzah. Here are some screenshots of the website that my circuit was supposed to be serving. I was able to control a whole strip of neopixels during my testing. 

![picture of final site]({{ site.baseurl }}/assets/homemadehardware/final-website-drop-down.png)

![picture of final site more info]({{ site.baseurl }}/assets/homemadehardware/final-website-info.png)

Keep reading to see the process of building my circuit.

<!--more-->

I started off with this design with 16 LEDs. The schematic looked good.

![original eagle schematic]({{ site.baseurl }}/assets/homemadehardware/final-first-schematic.png)

The board I designed is great with only two air wires and 0.5mm copper traces.

![original eagle board design]({{ site.baseurl }}/assets/homemadehardware/final-eagle-first-board.png)

Only problem is that when I imported my board from Eagle to Bantam it didn't include the solder pads for components. Only the traces were milled, which left little space for my components to sit on. Youc an see it on one of my boards that came off the Othermill bed.

![picture of the board that came off the othermill bed]({{ site.baseurl }}/assets/homemadehardware/final-failed-circuit-see-traces.jpg)

Of course, I tried to solder my tiny little SMD parts on anyways. I even made a solder stencil using the laser cutter. This is what my Illustrator file looked like, and then I used the 50W Epilog at 10% speed and 12% power to raster the plastic transparency paper.

![picture of solder stencil]({{ site.baseurl }}/assets/homemadehardware/final-solder-stencil-traces.png)

 After putting my SMD parts on, it didn't work out so well. I am pretty sure that because there were no copper pads for the LEDs to rest on, the metal terminals on the LEDs connected the data and power lines to the ground plane. I had two failed attempts ):

![picture of two failed boards]({{ site.baseurl }}/assets/homemadehardware/final-first-board-not-working.jpg)

In an attempt to save my project and try one last time, I made a new design with copper traces 1mm wide and reduced by 4x4 LED grid to a 3x3 grid. I made the board bigger to accommodate the larger traces and made sure that the pads showed up in the Bantam software.

![picture of new eagle schematic]({{ site.baseurl }}/assets/homemadehardware/final-second-schematic.png)

Honestly, I have no idea why the copper pads for my components show up only sometimes in Bantam. It takes a bunch of fiddling around to get Bantam to match what I designed in Eagle. I really dislike Bantam's software and I think if I'm going to acid etch my circuits in the future. But after a bunch of nonsense, I got it to final cut the way I wanted it to.

![picture of new eagle board design]({{ site.baseurl }}/assets/homemadehardware/final-eagle-second-board.png)

From there, I followed the process of adding the solder paste and using the pick-and-place machine. I did reflow and it looks good so far. I was waiting on new ESP8266 modules in the mail, so I hadn't soldered those on yet. At this point, I was pretty sure things were going to work out.

![picture of board with out IC module]({{ site.baseurl }}/assets/homemadehardware/final-side-by-side-failures.jpg)

Before soldering on my ESP8266, I taped off the end of the module in case any of its copper pads might cause a short with the traces on my board. And then I soldered it on.

![taped off wifi IC module]({{ site.baseurl }}/assets/homemadehardware/final-esp8266-tape.jpg)

I was able to get the code to upload after putting it into bootload mode.

![gif of the code uploading]({{ site.baseurl }}/assets/homemadehardware/final-code-uploading.gif)

All of this seemed good, but then when I reset the ESP8266 to run the code it kept outputting error messages like this. All the while, the blue LED on my ESP8266 was blinking every time it sends the error messages to the Serial monitor.

![gif of the serial monitor]({{ site.baseurl }}/assets/homemadehardware/final-serial-monitor-error.gif)

I also got errors like this about the reset.

![more error messages]({{ site.baseurl }}/assets/homemadehardware/final-more-error-messages.png)

I know that the chip is at least somewhat working since I was able to use [esptool.py](https://github.com/espressif/esptool) to get the MAC address and communicate with the chip a little bit.

![it kind of works???]({{ site.baseurl }}/assets/homemadehardware/final-trying-esptool.png)

It is possible that there is something wrong with my pull up or pull down resistors. Or maybe some kind of power issue. I did test all the voltages and did a very thorough continuity beep test. It is also possible that there is something wrong with the firmware. I tried using esptool.py to erase the flash and upload new firmware, but I'm not really sure if that did anything.

So close, yet so far. I spent many hours trying to debug it. Who knows, in the end maybe there is something wrong with the chip itself since I [bought it off Amazon](https://www.amazon.com/gp/product/B01M4IOFIT/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1) and it didn't even appear to be cut off a reel.

Eventually, I may return to it. I'm still unsure if there if there is a simple fix (replace the ESP8266?) or if it is something more complicated. I am thinking about revisiting it during the summer to fix it. I think that this project would be great as a larger scale interactive LED piece since people in class seemed to have a little bit of fun using the 2 LED version from my prototype.
