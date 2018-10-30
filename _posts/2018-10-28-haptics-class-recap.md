---
layout: post
title: Haptics Class Recap
date: 2018-10-28
type: post
categories:
- Haptics
tags:
- Sensors
- Motors
- Haptics
meta:
author:
   Beverly
---

![gif of haptic motor]({{ site.baseurl }}/assets/haptics/haptic-motor.gif)

This weekend (Oct 27-38), I was in the one-credit Haptics class w/ Kate Hartman. Overall, it was fun to learn about the vibration motors and play with different applications.

<!--more-->

### Experiment 1: Vibration Motors

Dongphil and I started by setting up the motor simply with the blink sketch. We played with changing the delay between when the motor was activated (set to HIGH voltage) and when it was off (set to LOW voltage). We had the following observations:

- The smallest pulse at high voltage we were able to feel when holding the motor was 50ms  
- We couldn’t feel the pulse at 10ms high voltage, but you can see it move a little bit
- Hands are the most sensitive to feeling the motor vibration
- We tested arm, tongue, and back of hand which was not as sensitive
- Experimented with the sound of the motor vibrating on different materials - table, plastic bag, foam plate, glass cup. Could be used to make percussive sounds.

Next, we added the transistor to the circuit to see how it would affect the strength of the motor vibration. We set it up using the TIP210 and a 1N400x diode.

![image of transistor circuit diagram]({{ site.baseurl }}/assets/haptics/haptic-transistor-circuit.png)

This definitely increased the strength of the vibration of the motor. It was strong enough that we could feel the vibration from across the table when it was pushed against the table surface. We also tried using one of the bigger vibratino motors that Kate brought.

![big motor with transistor circuit]({{ site.baseurl }}/assets/haptics/transistor-circuit-with-big-motor.jpg)

Next we tried the standard fade sketch, and played around with changing the step size and delays. It was more satisfying when the step size of the voltage increase was smaller. The smoothness of the vibration was super soothing and meditative.

### Experiment 2: Haptic Driver

![big motor haptic driver]({{ site.baseurl }}/assets/haptics/haptic-driver-big-motor.gif)

We borrowed Kate's [Adafruit DRV2605L Haptic Motor Controller](https://www.adafruit.com/product/2305) and tried the "basic" example sketch that runs through the different vibration sequences. They went by really quickly so it was kind of hard to differentiate when each was so short.

We also tried the "complex" example sketch to string together our own combinations of the vibration patterns. It was interesting how many combinations you could make and how a small change can totally alter the character of the vibration.

![haptic piezo]({{ site.baseurl }}/assets/haptics/piezo-motor-tap.gif)

We also used the "in" pin on the driver. In the documentation, you can use it to input an audio signal, but we use the "audio" example sketch and hooked up a piezo sensor. It basically functioned like a button - when you tap on the piezo it activates the haptic motor. This was a cool way to get an immediate interaction very quickly.

![haptic driver with piezo]({{ site.baseurl }}/assets/haptics/haptic-driver-piezo.jpg)

### Experiment 3: Motor Array

![motor array]({{ site.baseurl }}/assets/haptics/motor-array-small-motors.gif)

For the motor array, we played with the idea of having the feeling of rain on your hand. We first tested having the haptic motors take turns in order vibrating for one second each. And then we tried to see how it felt it they were going off randomly for random amounts of times. Dongphil made a strap to hold the foam plate against your palm to test how it close it would feel to rain.

![array w/ big motor]({{ site.baseurl }}/assets/haptics/motor-array-big-motor.jpg)

Because the motor vibrates it doesn't feel like a single point of pressure, but rather multiple taps. We also tried adding the big motor in the mix to see if that changed the sensation. It made it too heavy though, which doesn't really fit the sensation of rain drops. I think moving forward, it would be help to play with the form of the plate and placements of the motors.

### Experiment 4: Haptics Buffet / Cat Petting Simulation

![petting cats]({{ site.baseurl }}/assets/haptics/petting-cat-fur-hands.gif)

My group (Lin, Noah, Caleb, and Heng) wanted to work on haptics that were trigger by the user. I had the idea to recreate the experience of petting a purring cat. We decided it would be best to use large square pressure sensors along with the small haptic motors.

![cat group]({{ site.baseurl }}/assets/haptics/group-cat-pet-assembly.jpg)

We arranged it so that there were three equally spaced motors with the FSRs in between. This seemed to be effective, but didn't give us full coverage of the cat area.

![electronics inside]({{ site.baseurl }}/assets/haptics/under-cat-fur-sensors.jpg)

It was difficult to get everything connected since the motor wires were so small and the FSRs had those little leads. We ended up having a lot of alligator clips for the motors and modifying some female header jumpers for the FSRs. Caleb wrote the code, and we had to play making the FSRs sensitive to coming through the fur. We lowered the threshold so it would activate the motors using lighter pressure.

![final experiment]({{ site.baseurl }}/assets/haptics/petting-cat-fur.jpg)

Overall, people seemed to feel like it was enjoyable to pet our fake cat fur since you get all the joy of petting a cat's belly without the bites or scratches. There is something relaxing in feeling the purring sensation, and our team is planning to meet again to make a better version for the final project!
