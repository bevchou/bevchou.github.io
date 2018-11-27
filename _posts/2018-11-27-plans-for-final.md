---
layout: post
title: Plans for Final
date: 2018-11-27
type: post
categories:
- Temporary Expert
tags:
- Air
- Research
meta:
author:
   Beverly
---


I'd like to create a small ecosystem inside of a tall terrarium that mostly consists of air cleaning plants and layers of urban detritus in the lower section. I'll have a site that allows people to purchase rights to volumes of air/space inside of my enclosure. They can affect the air by "polluting" into the ecosystem at a fixed rate per square inch if they choose to engage in development activities that have a return on investment.

![sketch]({{ site.baseurl }}/assets/temp-exp/terrarium-sketch.jpg)

If I have time, I'd like to try to implement a way for people to buy & sell their air rights after the initial sale has finished. I wanted to use actual money, but I'm struggling to find a way to automate the exchange of small amounts of money for this system. I think I'd either need to find an alternate source of currency (like bits of personal info or fake $) or have a more manual exchange (like approving users after a Venmo exchange). In the spirit of making it more accessible, I will probably use fake currency. The system will be very simplified.

![values]({{ site.baseurl }}/assets/temp-exp/values-system.jpg)

Essentially, I want to create a mini-economic system where a group of people vie for control over the air. Some people will be preservationists who will choose not to harm the ecosystem and others who are seeking to generate short term value won't care. My "public" is people who think that individual action is making the greatest impact on improving the environment. My goal is to create an awareness of how economic systems do affect the environment by visualizing the tension between preservation and endless growth capitalism.

## Technical Stuff & Implemetation

I'd like the site to have a kind of bureaucratic look that is on par with other government websites. Here's an example of the vibe that I'm going for.

![example]({{ site.baseurl }}/assets/temp-exp/website-example.png)

Except, the inputs would be more related to filling out a form to purchase the air rights.

![drawing]({{ site.baseurl }}/assets/temp-exp/website-sketch.jpg)

I'm planning on implementing this using HTML/CSS and javascript. I'd run a node server to handle the user submissions on the back end. I will write a simplistic algorithm to handle how currency is allocated amongst users in the system. The node server would be on a computer (or [raspberry pi](https://www.w3schools.com/nodejs/nodejs_raspberrypi_gpio_intro.asp)) that is controlling the p comp system that is releasing the "pollution" based on the collective user input. I've found a tutorial from Kathleen McDermott to [modify vapes pens to produce a smoke effect](https://urbanarmor.org/portfolio/the-social-escape-dress/) that I will try. She ran the junk hacking workshop earlier this semester & it seems doable after gathering the necessary materials.  

**Time???**

Wow, this seems like a lot of stuff to get done. I'm pretty sure that I'll run into some issues implementing this and might need to scale down at some point. Maybe not. I may be combining the web/server development side with my live web final.

## Links for References

- Technical Stuff
  - [Making little fog machines](http://valkyriestudios.net/making-a-mini-fog-machine/)
  - [fog machine controlled by arduino Kate McDermott](https://urbanarmor.org/portfolio/the-social-escape-dress/)
  - [raspberry pi gpio control](https://www.w3schools.com/nodejs/nodejs_raspberrypi_gpio_intro.asp)
- Aesthetic
 - [nyc property search](https://nycprop.nyc.gov/nycproperty/nynav/jsp/selectbbl.jsp)


<!-- tall terrarium/tank w/ air cleaning plants
modify some vape pens to produce "pollution"



create a bureaucratic looking website where people can create a log in
and buy volumes of air in the tank in which they can choose among some activities that will pollute into the tank -->
