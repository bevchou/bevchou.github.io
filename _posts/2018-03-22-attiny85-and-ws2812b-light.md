---
layout: post
title: AtTiny85 and WS2812B Light
date: 2018-03-22
type: post
categories:
- Homemade Hardware
tags:
- ATtiny85
- Eagle
- NYU-ITP
- Othermill
- Soldering
- WS2812B
- LEDs
author: Beverly
---

![completed circuit working]({{ site.baseurl }}/assets/homemadehardware/midterm-working-image.jpg)

I made a light that reacted to the external environment. I decided to use a photo-resistor and a temperature sensor to determine the color and brightness of the lights. I was inspired by Magritte's painting "The Banquet" that I saw in Chicago last week.

I added some mounting points to mount material that will diffuse the light. There's also a larger hole so this light can hang on a wall. I haven't made the enclosure yet, but I'll update the post when I do. I'm waiting for the snow storm to stop before I try to go to Canal Plastics... Keep reading for exciting gifs, troubleshooting, Eagle screenshots, and more!

<!--more-->

Here's an initial sketch with my idea.

![sketch of midterm idea]({{ site.baseurl }}/assets/homemadehardware/midterm-sketch.jpg)

Next, I put together my Eagle files. Doing the schematic was simple. I initially had a 5V regulator, but Andy told me USB is always 5V! This was great news, so I was able to eliminate on extra part.

![Eagle schematic for midterm]({{ site.baseurl }}/assets/homemadehardware/midterm-eagle-schematic.png)

I made my board using the methods we talked about in class. Using the "polygon" tool to create a boundary around the board, naming it "GND", and then using "ratsnest" to flood the board with ground. Unfortunately, I have one air wire ): but overall, it came out how I wanted.

![Eagle schematic for midterm]({{ site.baseurl }}/assets/homemadehardware/midterm-eagle-board.png)

One of the biggest frustrations I had with this project was dealing with Bantam Tools' software for the Othermill. There were two main issues I ran into.

1.  It doesn't recognize lines drawn using "circle" in Eagle on the dimension layer. It won't cut them. This one had an easy workaround. Use "arc" instead of "circle" in Eagle.

2. It adds or doesn't show traces I've made in Eagle. I'm not sure what the pattern is with this error, but it is NOT COOL. It's totally fine here in Eagle.
![AtTiny85 close up in Eagle board]({{ site.baseurl }}/assets/homemadehardware/midterm-attiny-eagle-closeup.png)
Then after importing it in Bantam Tools and making sure I'm using all the right bits, it's like huh????
![AtTiny85 close up in Eagle board]({{ site.baseurl }}/assets/homemadehardware/midterm-attiny-bantam-closeup.png)
Well, I didn't figure out a great solution, so I ended up scraping away the excess copper between those two data pins with an Xacto knife.

Anyways, the circuit came out as expected on the Othermill.

![circuit board without components]({{ site.baseurl }}/assets/homemadehardware/midterm-board-no-components.jpg)

I had a combination of surface mount and through-hole components. I did the SMD parts first, adding solder paste by hand and the using the pick-and-place. Then, I used the heat gun for the reflow. Finally, I soldered the through-hole parts.

![circuit board with components]({{ site.baseurl }}/assets/homemadehardware/midterm-board-w-components.jpg)

I had some problems with my circuit when I finally got the code onto the AtTiny85. Only one LED would light up when running the "simple" example in Adafruit's Neopixel library.

![circuit board not working]({{ site.baseurl }}/assets/homemadehardware/midterm-one-led.gif)

Other people had similar issues, and [this thread on Adafruit's forums](https://forums.adafruit.com/viewtopic.php?f=47&t=69319) was the most helpful. I discovered that the key using the AtTiny85 with neopixels is to make sure you set the clock to 16 MHz. Here are the settings that worked for me when burning the bootloader.

![optimal AtTiny85 + WS2812B bootloader settings]({{ site.baseurl }}/assets/homemadehardware/midterm-attiny-bootloader-settings.png)

It works now!

![gif of LEDs lighting up using simple example]({{ site.baseurl }}/assets/homemadehardware/midterm-led-working.gif)

I am still working on refining the code (and I think my photoresistor isn't full soldered on since it's so noisy looking). I used the [Adafruit Neopixel Library](https://learn.adafruit.com/adafruit-neopixel-uberguide/arduino-library-use) which has a lot of great documentation with it. I'll post an update when I have the code finished up and the enclosure made.
