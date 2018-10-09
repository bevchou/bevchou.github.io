---
layout: post
title: Soft Sensors Class Recap
date: 2018-10-5
type: post
categories:
- Soft Sensing
tags:
- Sensors
- Sewing
- Soft
meta:
author:
   Beverly
---

This past weekend (Sept 29-30), I was in the Soft Sensors class w/ Kate Hartman. Overall, I learned a lot and here I'll go over what we did.

## My First Soft Circuit

![led soft circuit]({{ site.baseurl }}/assets/soft-sensing/my-first-soft-circuit.jpg)

The first thing we did was make a simple soft circuit that had a battery, conductive thread, and an LED. This was pretty straightforward and making the connections to the terminals on the battery and LED were easier than I thought it would be.

<!--more-->

## Testing Resistive Materials

Next, we tested the different properties of different resistive materials using a multimeter and reading in values from an Arduino.

### Multimeter Material Testing  

![led soft circuit]({{ site.baseurl }}/assets/soft-sensing/material-test-with-multimeter.jpg)

One of the things Alan and I noticed was how variable the values were. Especially for the stretch sensing material, it would never fully return to its original resistance because the material doesn't spring back to its original condition. Similarly, there are inconsistencies with these materials that depend on how they are manipulated. Pushing, stretching, compressing, and how the material give varying results.  

![bending the velostat]({{ site.baseurl }}/assets/soft-sensing/testing-material-w-multimeter.jpg)

We weren't able to precisely replicate the same movement every time. I think when it comes to soft sensors with these materials, a lot of adjustments need to be made in code. Also, as we found in class between different teams, so that meant the size of the material must be causing variations too.

### Arduino Material Testing

![material test results]({{ site.baseurl }}/assets/soft-sensing/material-test-with-arduino.jpg)

We had similar results with the materials' behaviors when reading the Arduino values. We tried to match the pull down resistor to the resistance from the multimeter tests, but the ranges (out of a maximum of 0-1023) was not as big as we hoped it would be. So when coding, it is helpful to use the map function.

![pressure sensing material]({{ site.baseurl }}/assets/soft-sensing/test-with-arduino.jpg)

Sometimes a bending motion could produce similar readings as pressure on the material. I think if you are testing  certain kind of movement you'll need to constrain other types of movement. For instance, if you only want to test pressure, you should mount the sensor to a flat, hard to bend surface.

## Sensor Sprint

Caleb, Erin, and I worked together on the sensor sprint. We made a couple pom-pom sensors, which I was pretty excited about. We used these pom-pom makers.

![pompom maker]({{ site.baseurl }}/assets/soft-sensing/making-a-pom-pom.jpg)

And ended up with these. We tried to use the conductive fiber as well as just conductive thread mixed with regular yarn. I think the fiber worked better because it was more voluminous.

![pompoms]({{ site.baseurl }}/assets/soft-sensing/conductive-pom-poms.jpg)

On their own, they react pretty well to being compressed. But I can imagine them being used with more conductive material to creative different results.

![pompom bb]({{ site.baseurl }}/assets/soft-sensing/pom-pom-led.gif)

We also made a simple pressure sensor using the Eeonyx material. I creative a wavy pattern with the conductive thread and taped it onto both sides. I left some of the thread sticking out so we could connect alligator clips to the Arduino.

![pressure sensor]({{ site.baseurl }}/assets/soft-sensing/punch-meter-sensor2.jpg)

We put the sensor into a foam punching glove that Erin made, so you can see how hard you've punched something.

![punch sensor]({{ site.baseurl }}/assets/soft-sensing/punch-meter-sensor.jpg)

## Sensor Research

Jenna, Caleb, Alan and I worked together to make a soft sensing cat toy. We were inspired by some of the examples we found on [How to Get What You Want](https://www.kobakant.at/DIY/). We liked the [stroke sensor](https://www.kobakant.at/DIY/?p=792) and used it as the inspiration. Instead of sewing the conductive "hairs" to attach to a piece of conductive fabric, we sewed them into some conductive fiber. This added another way to change the resistivity of the overall toy. We hoped that the sensor would react to being squeezed (through the change in resistance from the fiber) and also being touched (by the change in resistance from the conductive thread hairs). All of the fiber was was sewn into some fur fabric we found in the soft lab.

![jenna sewing sensor]({{ site.baseurl }}/assets/soft-sensing/making-experimental-sensor.jpg)

 We had to tweak the way we mapped the voltage to connect to an LED. We also had some conductive fabric ears that we connected the alligator clips to. This is the set up for our Arduino.

![arduino circuit]({{ site.baseurl }}/assets/soft-sensing/arduino-set-up.jpg)

And in the video you can see the resistance is changing as the toy is moved and touched in different ways.

![gif of cat toy sensor]({{ site.baseurl }}/assets/soft-sensing/experimental-sensor-loop.gif)

I think they toy could be used to make unpredictable changes that would entertain a cat or maybe the the owner know that the cat is playing. This sensor was more so a fun experiment than an actually a good cat toy. It was interesting to see that the conductive hairs connected to the fiber were able to create measurable change, and we'd have to experiment more with the code to account for the changing readings as the fiber gets more compressed.

Overall, the class was really fun and a great introduction to these materials. I'm excited about the "perfect sensor" which I will post about soon! (:



<!-- Final Workshop
Caleb, Jenna, Alan, Beverly

Cat Toy Sensor

We made a sensor that reacts to pressure and stroke

We found some fur fabric and stuffed it with the conductive fiber. Inspired by this [stroke sensor](https://www.kobakant.at/DIY/?p=792), we created some "hair" using conductive thread. These conductive threads are also in contact with conductive fiber inside the toy. -->
