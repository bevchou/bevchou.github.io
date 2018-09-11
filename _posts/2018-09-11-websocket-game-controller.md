---
layout: post
title: Websocket Game Controller
date: 2018-09-11
type: post
categories:
- Understanding Networks
tags:
- WiFi
- ESP8266
- TCP
- Controller
meta:
author:
   Beverly
---

This post is still in progress!!

![image of controller]({{ site.baseurl }}/assets/und-networks/websocket-controller-final.jpg)

I used the Feather Huzzah ESP8266 board to create my game controller. Here is an overview of what is happening in the code at a high level.

1. Connecting to the itpsandbox WiFi network.
2. Using a button to activate the connection to the server.
3. An LED inside the button will indicate when the controller is connected.
4. Rotary encoder dials on the top and side let the user scroll their paddle up/down and left/right.
5. When you're done playing the game, you can hit the button again to disconnect.

Here's a video of the breadboard prototype working.

<div class="responsive-container"><iframe src="https://player.vimeo.com/video/289219307" width="640" height="1138" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

Click more to see the full code.

<!--more-->

<script src="https://gist.github.com/bevchou/1aedf7938a7c4e9e1da9b3281ab188dd.js"></script>
