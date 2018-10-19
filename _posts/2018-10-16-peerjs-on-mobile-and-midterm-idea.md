---
layout: post
title: PeerJs on Mobile and Midterm Idea
date: 2018-10-16
type: post
categories:
- Live Web
tags:
- Midterm
meta:
author:
   Beverly
---

My idea for my Live Web midterm is to make a site that collects video clips or images based on a 24 hour cycle of time. So when you are on the site, it would play whatever users recorded at that time. Or if no one had recorded anything, you could add something. If multiple people are on the site at once, you'll be be able to see them in real time. It would basically be a clock where the time is told via photos or videos.

<!--more-->

I think that it's not possible to store videos, so for now I'm going to focus on having users capture images. I wanted to have it be possible for people to capture photos from their smartphones so that it wouldn't necessarily be a selection of selfies, although that would be fine.

Some examples of websites that used 24 hours of media are Pharrell's Happy music video. Basically, the song played on loop (annoying, I know) while a 24-hour-long video of dancers at various times/places ran.

![]({{ site.baseurl }}/assets/live-web/24-hour-happy-pharrell.jpg)

Another website that plays with the idea of time is [here is today](http://hereistoday.com/). It shows you a slice of today and then moves to bigger and bigger units of time.

![]({{ site.baseurl }}/assets/live-web/here-is-today.png)

Neither of these websites uses live media and interaction, so hopefully I can create something fun. Because I'd like for users to capture images out in the world beyond their laptop webcam, I needed to get Peer Js to work on phones. I own an iPhone, so I got it to work there, but I am not 100% sure about other devices.

Even though [they say it can't be done](http://iswebrtcreadyyet.com), Roland helped me get PeerJS and WebRTC to work on mobile Safari. The secret is in the [video policies for iOS](https://webkit.org/blog/6784/new-video-policies-for-ios/). To get the videos to play, you need to have these attributes set to true on the video.

{% highlight html %}
<video id="myVideo" playsinline controls="true" autoplay></video>
{% endhighlight %}

And if you're generating video elements in javascript, make sure you add these attributes to your new video elements!

{% highlight javascript %}
videoElement.autoplay = true;
videoElement.controls = true;
videoElement.playsInline = true;
{% endhighlight %}

And then it works & you can chat with yourself from multiple angles while you test it. Hoping that I can implement this in my midterm along with figuring out a database system. I'd like to have the user use the outward facing camera, so I'll need to look into that too.

![]({{ site.baseurl }}/assets/live-web/peerjs-on-phone.png)
