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

I changed my self portrait because the first one had a video that was unnecessarily enoorrrrmous and it was sort of boring. Now I have a smaller video file and you can make me say whatever want using the [100 most common words in English](https://en.wikipedia.org/wiki/Most_common_words_in_English) according to Wikipedia. I'm imagining this would be fun on a tablet and it might be even more fun if I added some more colorful words.

[Click here to play!](https://itp.beverlychou.com/live-web/2018_9_10_BetterSelfPortrait/)

<!--more-->

The important bit of code that lets you control the video with the buttons is below. I looped through an array of 100 words called "words[]", and each time I create a button that called a function when clicked. The function's input is the word's index.

{% highlight javascript %}
for (let i = 0; i < words.length; i++) {
  let buttonHTML = "<button onclick='setVidTime(" + i + ")'>" + words[i] + "</button>";
  buttons.innerHTML += buttonHTML;
}
{% endhighlight %}

I timed my video so I say a new word every 1.5 seconds - I used a metronome. Then I can set the video's current time to play back at the word associated with that button. I start the video little before to account for any inconsistencies in the video and then pause it before the next word.

{% highlight javascript %}
function setVidTime(wordNum) {
  video.currentTime = wordNum * 1.495;
  video.play();
  setTimeout(function(){ video.pause(); }, 1450);
}
{% endhighlight %}

Read more for my experience using Nextdoor.

![nextdoor mainpage]({{ site.baseurl }}/assets/live-web/nextdoor-mainpage.png)

For my synchronous site, I tried using Nextdoor. It is essentially a hyperlocal Facebook where people mostly post about cats. I signed up using a code I got in the mail on a physical postcard. I'm assuming this is how they knew my location and connected me into the right community of people. It's interesting that the location of your home and your real name are used. I blurred out the names/locations in my images because of this.

It feels like a glorified neighborhood cork board you would find in a coffee shop. The posts aren't terribly exciting, but it's good if you need to sell/buy something, find a lost pet, get some local suggestions, be alerted of petty crime, and talk to some people in your neighborhood. It is a great place to post about cats!!! People post about good cats.

![good cats]({{ site.baseurl }}/assets/live-web/nextdoor-cat1.png)

People also post about bad cats.

![bad cats]({{ site.baseurl }}/assets/live-web/nextdoor-cat2.png)

Overall, I like that there is a genuinely helpful vibe and I don't see anyone abusing the site. I think that might be due to the fact that there is no anonymity. I hope the site isn't using the info for anything creepy though.

 I do find it a weird that instead of meeting your neighbors in person, someone thought we needed this online interaction. In some ways, this site is actually useful, but honestly, I think social anxiety only heightens when we rely on online socialization like this. I mean I'm guilty of it too sometimes, but for me I'm not trying to live in weird hyperconnected isolation. I have a lot of thoughts on that, but I'll save it for another time.
