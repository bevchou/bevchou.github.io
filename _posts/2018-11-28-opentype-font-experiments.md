---
layout: post
title: Opentype Font Experiments
date: 2018-11-28
type: post
categories:
- Computational Approaches to Typography
tags:
- Javascript
- Bluets
meta:
author:
   Beverly
---

<!-- {{ site.baseurl }} -->

![demo gif]({{ site.baseurl }}/assets/comp-typo/opentypejs-demo.gif)

[Click here to go to project.](https://itp.beverlychou.com/computational-approaches-to-typography/4_opentype/)

I experimented with using font outline data to create some simple reactions to the user. In the second row, the mouse position causes the straight lines in each letter to warp towards the mouse. In the third row, the more you click the more the lines expand away from the curves.

I played with a couple different kinds of font data this week before getting to this point, but I didn't really document it ): I took a look at how the [Hershey fonts](https://github.com/techninja/hersheytextjs) data worked because I really liked the name of all the fonts and the old school feel. The main thing to know about this Hershey font data is:

- "M" is move your metaphorical pencil to that position
- "L" is draw a line to that position from the previous position

Each coordinate comes with an "M" or "L", so it's pretty straightforward. There's no need to worry about filling in the letter since it's only made of lines. [Allison's code](https://editor.p5js.org/allison.parrish/sketches/SJv2DCYpQ) for this is really helpful and playing with the Hershey fonts first helped me understand [Opentype.js](https://github.com/opentypejs/opentype.js) more. Essentially, the thing to know about this data is:

- "M" is move your metaphorical pencil to that position
- "L" is draw a line to that position from the previous position
- "C" is draw a bezier curve, which only works for OTF
- "Q" is draw a quadratic curve, which only works for TTF
- "Z" is to where to end the path

I did try the [example code for the filled-in, animated letters](https://editor.p5js.org/allison.parrish/sketches/Hy3-Iqm67), but liked dealing with the outlines much more. So I started with [this of example code to draw letter outlines](https://editor.p5js.org/allison.parrish/sketches/BklobgCO67).

<!--more-->

Here is the key code snippet for the warping letter is this.

{% highlight javascript %}
//IN THE FUNCTION THAT DRAWS THE LETTERFORMS FOR SECOND ROW
case 'L':
  //draw bezier instead of a line and warp it based on the multiplier values calcualted in the draw function
  // line(cx, cy, cmd.x, cmd.y);
  bezier(cx, cy, cx * multiplierX, cy * multiplierY, cmd.x * multiplierX, cmd.y * multiplierY, cmd.x, cmd.y);
  cx = cmd.x;
  cy = cmd.y;
  break;
{% endhighlight %}

Here is the code for the expanding letters.

{% highlight javascript %}
//IN ANOTHER FUNCTION THAT DRAWS THE LETTERFORMS FOR THIRD ROW
case 'L':
  //draw line to this position
  //translate further based on how many times the user clicks on the page
  let translateLine = {x: mouseCount*5, y: mouseCount*5};
  line(cx + translateLine.x, cy + translateLine.y, cmd.x+translateLine.x, cmd.y+translateLine.y);
  cx = cmd.x;
  cy = cmd.y;
  break;
case 'C':
  //draw bezier curve (otf)
  //translate further based on how many times the user clicks on the page, move in opposite direction of lines
  let translateBez = {x: -mouseCount*5, y: -mouseCount*5};
  bezier(cx + translateBez.x, cy+ translateBez.y, cmd.x1+ translateBez.x, cmd.y1+ translateBez.y, cmd.x2+ translateBez.x, cmd.y2+ translateBez.y, cmd.x+ translateBez.x, cmd.y+ translateBez.y);
  cx = cmd.x;
  cy = cmd.y;
  break;
{% endhighlight %}

All of the code is available on my github [here](https://github.com/bevchou/computational-approaches-to-typography/tree/master/4_opentype).
