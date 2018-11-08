---
layout: post
title: Asemic Writing
date: 2018-11-6
type: post
categories:
- Computational Typography
tags:
- Javascript
- p5.js
meta:
author:
   Beverly
---

<!-- {{ site.baseurl }} -->

![demo gif]({{ site.baseurl }}/assets/comp-typo/asemic-text.gif)

[Click here to go to project.](https://itp.beverlychou.com/computational-approaches-to-typography/2_Asemic_Text/)

The asemic writing I created is based on more western languages where it appears to go left to right and has distinct separate words. It is clearly my bias to do something western-looking as someone who is a native English speaker. I was influenced by [Vera Molnar's Lettres de ma mére](http://dam.org/artists/phase-one/vera-molnar/artworks-bodies-of-work/lettres-de-ma-m-re). Here is one of the pieces in this series.

![vera molnar]({{ site.baseurl }}/assets/comp-typo/vera_molnar_lettres_de_ma_mere.jpg)

I liked the layering of different colors and the erratic-ness of the lines. I tried to imitate it by using the random function to continually change the amplitude and angle of a sine wave. I plotted these at varying lengths to create different words and then tried to have it start a new line when it hit the margin of the canvas.

All of the code is available on my github [here](https://github.com/bevchou/computational-approaches-to-typography/tree/master/2_Asemic_Text).
