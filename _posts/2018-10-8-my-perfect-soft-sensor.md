---
layout: post
title: My "Perfect" Soft Sensor
date: 2018-10-8
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

![]({{ site.baseurl }}/assets/soft-sensing/almost-finished-sensor.jpg)

My sensor is a series of pressure sensors in a row that is designed to be able to pick up different gestures. I haven't written more complex code to sense different movements, but the idea is that you could press in different patterns to do different things. For example, you could move your hand up/down to control something high to low. Or if you pressed and moved your hand in a specific range or pattern with varying pressures it could initiate some kind of response.

I need to work on adding features to sense different patterns in the code. Hopefully this fulfills the "beautiful" criteria. I think it looks okay, but it's more general purpose at this stage.

<!--more-->

### Process

I wanted to design a cleaner, more reliable sensor than the ones we did in class. Originally, I want to make something big. I was thinking about using velostat w/ a rug in my room to have it control things when I stepped on it. In the end, I went small because I don't have a big piece of velostat laying around. I was still interested in different ways that controls could be integrated into furniture items so I imagined creating a sensor that could be added to anything.

The pressure sensing strip started by getting the right materials. I used the Eeonyx Pressure material and some iron on conductive fabric strips. I knew I needed to make the sandwich (conductive-resistive-conductive) so I designed my sensor like this.  

![]({{ site.baseurl }}/assets/soft-sensing/perfect-sensor-sketch.jpg)

I got all my pieces lined up and made sure to leave some space where I could sew my conductive thread connections to.

![]({{ site.baseurl }}/assets/soft-sensing/pressure-sensor-strip.jpg)

Next, I sewed the connections. The patches of conductive material on the bottom are sewed separately on the right side of the strip. The long line of conductive thread on the left is to all connected so that it can be wired to ground. I tried to gather all the connections on the right side to make it easier. I tried to sew over the conductive fabric threads multiple times to secure the connection.

![]({{ site.baseurl }}/assets/soft-sensing/machine-sewing-connections.jpg)

I did a test on the resting state resistance and it was approximately 25 kilohm. So then when I wired the Arduino I had my pull up resistor at 22 kilohm. This brought the readings to around 450 when it was at its rest state.

![]({{ site.baseurl }}/assets/soft-sensing/perfect-sensor-arduino.jpg)

I mapped the individual values, but I'd like to implement some of the calibration code. I tried to cut the strips of conductive fabric all the same, but I guess there is still some variation and all of them probably do not overlap perfectly with each other. I did everything by hand and eyeballed it, but if I wanted something precise, I could use the laser cutter or a ruler.

```
int mappedA = map(sensorValA, 505, 300, 0, 10);
int mappedB = map(sensorValB, 550, 350, 0, 10);
int mappedC = map(sensorValC, 540, 360, 0, 10);
int mappedD = map(sensorValD, 510, 350, 0, 10);
int mappedE = map(sensorValE, 440, 290, 0, 10);
```

I was able to read in the values as I pressed each sensor. I regular press hit in around 3-4 reading, and then a really hard press would give you a 7-9 reading. You can tell it's a little bit noisy which I am pretty sure had to do with the way the wires are wrinkling my fabric when I wired it up. I think if I used wire wrapping or another connection method that is softer it would work better.

![]({{ site.baseurl }}/assets/soft-sensing/reading-each-input.gif)

Overall, it was nice to make a pressure sensor that is a little nicer looking. I brushed up on some sewing skills, and I am excited to make a soft sensor for something bigger in the future. At ITP space is limited, so now I'm excited to make something big that can roll up and fit in my locker! Or something wearable.
