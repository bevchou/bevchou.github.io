---
layout: post
title: Filling Out A Form Using A Voice Interface
date: 2018-03-07
type: post
categories:
- Voice Interfaces
tags:
- Interface
- p5 Speech
- p5.js
- Voice
meta:
author:
   Beverly
---
<p><div class="responsive-container"><iframe src="https://player.vimeo.com/video/258949736" width="640" height="626" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
</div></p>

[TRY IT HERE](http://itp.beverlychou.com/voice-interface-midterm/)

For my voice interface, I decided to go for a more functional route. Sometimes it is time consuming or feels cumbersome to fill out forms by typing or writing by hand, so I wanted to make an experience where a user can fill out a form quickly by speaking the answers. There's a demo video above and the full dialog flow is below.

![dialog flow]({{ site.baseurl }}/assets/voice-interf/Midterm-Dialog-Flow.png)

<!--more-->

### About the Dialog Flow
It starts pretty linearly, but you can get into different interactions when you ask for help and at the end when when confirming or changing your answers. I tried to make sure there were options that made the user feel in control.

I do think this is fine if you're filling out a form for the first time, but I imagine it gets annoying when you have to fill out many forms (or when you're debugging...). You don't always want to hear the intro spiel every time. I tried to balance this by providing enough direction and context and I also had the voice cancel if you interrupt it. This way you don't need to wait for it to finish talking if you don't want to.

## The Persona
I know I'm going broad with the persona description, but I'm going to say the persona for this VUI is a human that regularly fills out forms. I'm talking about filling out your info when you buy something online, sign up for events, do your taxes, data entry, etc. Things that are tedious to sit there and type or write out. Maybe as a first application - since STT isn't 100% confident, which is problematic for sensitive info - this would be great for filling out long review forms/psychology study style forms. I know I hate how long it takes to do those forms and I think this could be a way to speed up the process.

## Aesthetics
I am using the default p5 Speech voice and I haven't styled the website. For this version as a prototype, I am trying to get the concept across, however if I was making something higher resolution I would have taken a few extra steps to make it more friendly. The voice is too robotic to a point where it's a little hard to understand. The ideal voice to me is clearly a non-human, but still easy to understand. I also didn't have any phrases where the VUI tried to be funny or clever. I don't like that. It's not cool when an interface tries to get cute with me.

## Conclusions & Thoughts
First of all, I'm aware that using the p5 Speech library was not the most reliable method of STT and it doesn't have the nicest voice for TTS. I think the key elements are there for a VUI, but using something like the Google Voice API for STT and Watson for TTS would greatly improve the aesthetics. I did try to work within my skill set because I knew I could either make a low resolution, more fully developed VUI or a high resolution, less developed VUI.

Overall, I'm not a fan of VUIs that try to be too human. I think VUIs are more useful as something to improve efficiency rather than cultivate a sense of intimacy with technology. Like for instance it's faster and easier to ask for info from a (readily available, knowledgeable) person or a really great VUI, than to spend a bunch of time typing things into a search engine. However, I do think it's a problem if we start to replace those human-human interactions with human-VUI ones. We lose an important social aspect that I don't think is replaceable.
