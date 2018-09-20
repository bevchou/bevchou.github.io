---
layout: post
title: Web Self-Portrait
date: 2018-09-11
type: post
categories:
- Live Web
tags:
- Javascript
meta:
author:
   Beverly
---

![self portrait screenshot]({{ site.baseurl }}/assets/live-web/live-web-self-portrait-screenshot.png)

I changed my self portrait because the first one had a video that was unnecessarily enoorrrrmous and it was sort of boring. Now I have a smaller video file and you can make me say whatever want using the [100 most common words in English](https://en.wikipedia.org/wiki/Most_common_words_in_English) according to Wikipedia. I'm imagining this would be more fun on an tablet and it might be even more fun if I added some more colorful words.

[Click here to play!](https://itp.beverlychou.com/live-web/2018_9_10_BetterSelfPortrait/)

<!--more-->

The important bit of code that lets you control the video with the buttons is below. I looped through an array of 100 words called "words[]", and each time I create a button that called a function when clicked. The function's input is the word's index.

```
for (let i = 0; i < words.length; i++) {
  let buttonHTML = "<button onclick='setVidTime(" + i + ")'>" + words[i] + "</button>";
  buttons.innerHTML += buttonHTML;
}
```

I timed my video so I say a new word every 1.5 seconds - I used a metronome. Then I can set the video's current time to play back at the word associated with that button. I start a the video little before to account for any inconsistencies in the video and then pause it before the next word. 

```
function setVidTime(wordNum) {
  video.currentTime = wordNum * 1.495;
  video.play();
  setTimeout(function(){ video.pause(); }, 1450);
}
```
