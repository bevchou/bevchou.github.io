---
layout: post
title: Slow Net
date: 2019-08-07
type: post
categories:
- Thesis
tags:
- Thesis
meta:
author:
   Beverly
---

_This is an update on my ITP thesis! Slow Net is an ongoing project - see [slownet.work](https://slownet.work) for more._ 

## ITP Thesis Week 2019

Slow Net is a series of experiments that explore how slow networks can be used to protect against data-collecting entities that threaten our autonomy and influence our identities.

<iframe src="https://player.vimeo.com/video/336836245?byline=0&portrait=0" width="640" height="360" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Abstract

Privacy concerns have made many news headlines recently, and it’s become clear that our behavioral data is collected when we’re browsing online and using smart devices. Some of the data is used for improving user experience, but much of it is used to predict and influence our behaviors in real-time. By predicting what we’ll do next, data collectors can use the data to intervene and divert our actions in a direction that supports them economically. In this process, humans are reduced to interchangeable pieces of data in a homogenous population of data laborers. As a result, power and wealth is concentrated among those who are able to collect, utilize, and gatekeep vast amounts of information. Our identities get privatized and our autonomy is threatened.

Because real-time collection of data is enabled by fast Internet speeds, one form of resistance could involve co-opting a tactic from labor unions called the slowdown strike, in which workers deliberately reduce their productivity. My thesis project, Slow Net, aims to utilize this strategy of purposeful inefficiency in three pieces.

1. A zine called A Quick Guide to the Slow Net provides conceptual context to the problems underpinning data collection.
2. An online messaging application, Slow Chat, forces users to write longer messages and wait longer between messages as conversations progress.
3. A Slow Router provides free wifi at a much slower speed than expected.

Each of these pieces functions with the goal of slowing the capture of personal data, encouraging more intentional action, and creating opportunities for idle time that allow for introspection and self-development. Collectively these actions attempt to preserve our autonomy and identity. My hope is that as users we can reconsider our relationship with many of the internet platforms we use that exploit us, and as technologists we can re-examine our role in working with and developing these technologies.

## Context/Research

I originally started my inquiry by asking how we can build trust in our everyday technologies by exposing their underlying systems. I am fascinated with infrastructure and Hans Haacke’s work, especially "Condensation Cube", which exposes an invisible system in action. Haacke’s "Shapolsky Et Al. Manhattan Real Estate Holdings, A Real-Time Social System, As Of May 1, 1971" was my main inspiration in trying to map where our behavioral data goes after it gets collected. After reading Shoshana Zuboff’s "The Age of Surveillance Capitalism" and Jack Self’s article "Beyond the Self", I eventually diverged to focus on the impact of data collection because I was alarmed by the imbalance of power between users and data holders. Our current ITP resident Se¿o’s "Postcards Computer" and Kevin Roose’s New York Times article “Is Tech Too Easy to Use?” helped me to develop a rationale around how complexity and inefficiency can be used advantageously.

For A Quick Guide to the Slow Net, I was inspired by Mimi Onuoha and Diana Nucera’s "A People’s Guide to AI" and and Amy Wibowo’s "Bubblesort Zines". I really like how they discuss complicated technical ideas to broader audience. Slow Chat was largely inspired by my inability to text people back within socially appropriate timeframes. For the Slow Router, I looked to other artists using network infrastructure to resist against invasions of privacy like Trevor Paglen’s "Autonomy Cube" and Dhruv Mehrotra’s "Othernet".

## Technical Details

Slow Chat was created using Node.js, Express, and Socket.io javascript libraries. The Slow Router is a Raspberry Pi 3 B+ on Raspbian Stretch Lite operating system running hostapd, isc-dhcp-server, wondershaper, and nodogsplash.
