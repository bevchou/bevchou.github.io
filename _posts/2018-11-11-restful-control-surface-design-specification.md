---
layout: post
title: RESTful Control Surface Design - Specification
date: 2018-11-11
type: post
categories:
- Understanding Networks
tags:
- REST API
- HTTP Requests
meta:
author:
   Beverly
---

Alden and I are working on a control interface for people to [VJ](https://en.wikipedia.org/wiki/VJing). We surveyed a couple ITPers on the floor about what makes a good VJ set. People liked when:

- Visuals reflect the mood and emotional content of the music
- Timing matches the music
- You warn people if you're gonna do a strobe effect
- There is a dynamic arc or storyline to the visuals

Given our restraints, we knew that timing might be an issue since using REST might not provide instantaneous feedback needed for syncing up with music. Either way, we're still doing it. In our spec, we would like to have the following options for the controller that will output to visuals (in a browser) that can be projected or shown on a screen. These are the user inputs we'd like to have on the controller.

- gif mode (on/off)
  - keyword (text input)
- abstract visual mode (on/off)
  - movement speed (range)
  - foreground color (HSL range)
  - background color (HSL range)
  - shapes/patterns (set of options)
    - rect, circle, triangle, squiggle, arc

We want the clients to communicate according to this system diagram. We are planning on using the Giphy API to pull content for the "gif mode".

![img of system diagram]({{ site.baseurl }}/assets/und-networks/REST-system-diagram-for-VJ.jpg)

Either a physical or digital interface will work for the controller (:
