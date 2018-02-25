---
layout: post
title: TTS Command Line Interaction
date: 2018-01-31 18:29:54.000000000 -05:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Expressive Voice Interfaces
tags:
- node.js
- TTS
meta:
  _edit_last: '1'
  enclosure: "https://beverlychou.com/itp/wp-content/uploads/2018/01/itsworkingvideo.mov\r\n732417\r\nvideo/quicktime\r\n"
author:
   Beverly




---
<p><div class="responsive-container"><iframe src="https://player.vimeo.com/video/257323881" width="640" height="410" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
</video></div></p>
<p>For my TTS interaction, I have made a Node.js project that will give a user the weather when prompted. Read more below about it.</p>
<p><!--more--></p>
<p>I originally wanted to find an API that would be able to take images, and output a description of the image. I thought that it would be something practical for visually impaired people, however I do know that similar things (like reverse image search and accessibility apps) already exist. I just wonder how it would work the constraints given to us for this assignment. I attempted to do something with the knn image classification in deeplearn.js, but I wasn't able to find enough documentation to figure it out.</p>
<p>Once I accepted that I wouldn't be able to accomplish that with my current technical skills and after loosing several hours to it, I decided to use the <a href="http://openweathermap.org/current">OpenWeather Map API</a>. I thought that using a voice to convey data that changes is far more interesting than hard-coding a limited number of TTS responses. Going along with the idea of a voice interface being conversational, it makes a lot more sense that we would like to have responses that vary from time to time. While the weather isn't the most thrilling topic, I think it provides enough variability and functionality to keep things somewhat interesting.</p>
<p>My javascript code is below.</p>
<p><script src="https://gist.github.com/bevchou/a931e48ef21a7edfc44ec8d638ed2f99.js"></script></p>
