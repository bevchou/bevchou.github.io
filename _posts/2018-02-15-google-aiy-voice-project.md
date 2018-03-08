---
layout: post
title: Google AIY Voice Project
date: 2018-02-15 15:57:34.000000000 -05:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Voice Interfaces
tags:
- AIY Voice Kit
- Python
- Raspberry Pi
- Terminal
- Voice
meta:
  _edit_last: '1'
  enclosure: "https://beverlychou.com/itp/wp-content/uploads/2018/02/whereamivideo_compressed.mov\r\n6834319\r\nvideo/quicktime\r\n"
author:
   Beverly




---
<p><img class="alignnone size-full wp-image-614" src="{{ site.baseurl }}/assets/old-wp-content/voicekit.jpg" alt="" /></p>
<p>This week, I set up an <a href="https://aiyprojects.withgoogle.com/voice">Google AIY Voice Kit</a> with a Raspberry Pi. While building the box and putting everything together was pretty easy, I actually ran into several issues when trying to run code. Keep reading below to see the process, some code, and a video of it working.</p>
<p><!--more--></p>
<p>Particularly I continued to run into variations of this message over and over again.</p>
<p><img class="alignnone size-full wp-image-603" src="{{ site.baseurl }}/assets/old-wp-content/Screen-Shot-2018-02-10-at-7.26.53-PM.png" alt="" width="805" height="117" /></p>
<p>I went through the process of troubleshooting and looking up this segmentation issue. I attempted to update the raspberry pi and change various settings, which ended up not solving this problem. I am honestly not sure what the root cause of the problem was, but I ended up re-flashing my microSD card and only then was I able to get the examples to work.</p>
<p>I ended up setting up my raspberry pi headless (only used my macbook). This is honestly way more convenient that using the monitor, keyboard, and mouse. The only trouble is initially figuring out the raspberry pi's IP address. It's not too bad - you can just plug it into your router with an ethernet cord &amp; then log in to the router to find all the connected device's IP. Then you can ssh into the raspberry pi and set things up as normal. I also used xrdp so I could using my macbook to see the GUI through Remote Desktop Connection. This let me use the terminal to open web browser tabs (:</p>
<p>Following that, I had to figure out Python. Compared to JavaScript it looks like reading a book with no punctuation, but Jim's Python flyby on Friday was so amazingly helpful! I finally was able to understand the logic of the code, however I do think that <a href="https://github.com/google/aiyprojects-raspbian">Google's examples</a> need more comments and explanation! If we have time for that in class I would really like to go through that more thoroughly.</p>
<p>I also had this issue when I created python files using the "touch" command, the files would get a lot of errors. I ended up just copying (use "cp" in terminal) google's example files and editing it from there. <span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif; font-size: 1rem;">Anyways, here is the code where I added some of my own commands.</span></p>
<p><script src="https://gist.github.com/bevchou/9dbd01917eb3724e8f4b793a544a4edc.js"></script></p>
<p>I ran the command like so:</p>
<blockquote>
<p class="p1"><span class="s1">/home/pi/AIY-projects-python/env/bin/python /home/pi/AIY-projects-python/src/examples/voice/test1.py</span></p>
</blockquote>
<p>And here is what it looks like in action.</p>
<p><div class="responsive-container"><iframe src="https://player.vimeo.com/video/257325454" width="640" height="1129" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div></p>
<p>Maybe for the final I will use the voice kit to control some physical elements. I was looking at <a href="https://projects.raspberrypi.org/en/projects/google-voice-aiy">this tutorial</a> to control the GPIO pins, which might be fun.</div>
