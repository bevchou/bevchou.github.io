---
layout: post
title: Traceroute of My Most Visited Sites
date: 2018-09-28
type: post
categories:
- Understanding Networks
tags:
- Traceroute
meta:
author:
   Beverly
---

I started investivating by looking at what sites I visit most often. If you use Chrome, you can go to [chrome://site-engagement/](chrome://site-engagement/) and see which sites you use most frequently. It's a little creepy that Chrome is tracking your engagement on all the sites your browse, but really it's just the tip of the iceberg.

I'm interested in how location affects the traceroute, so I'm also going to compare Google in the US (google.com) and Google in Taiwan (google.com.tw). I also looked at my personal site (beverlychou.com), which is hosted through DreamHost, and my blog (itp.beverlychou.com), which is hosted through GitHub Pages. I think they'll go through different paths. The domain is from Namecheap, which points to DreamHost. From there the subdomain for my ITP blog points to GitHub pages. I collected data at three locations - ITP, my home, and a coffee shop with public wifi.

## Google.com vs Google.com.tw

![google]({{ site.baseurl }}/assets/und-networks/traceroute-google.jpg)

![my site engagement]({{ site.baseurl }}/assets/und-networks/traceroute-googletw.jpg)

I hypothesized that Taiwanese Google would try to go to IP addresses out in Taiwan, but I was totally wrong. The traceroutes between Google.com and Google.com.tw were nearly the same. The traceroute I did at ITP for both are identical except for the final IP address, both of which were in Mountain View. I think this indicates that all the versions of Google are actually hosted from their headquarters in Mountain View. A quick look at some other domains (Google.de, google.fr, google.ca, etc) show that the final hop ends on an IP located in Mountain View, CA.

Both the coffee shop and my apartment's wifi have Time Warner Cable as the ISP according to the data I collected. I was confused because we pay the bills to Spectrum. It turns out another company called Charter bought Time Warner Cable, and they rebranded as Spectrum. Both traceroutes try to go through Englewood, CO. All the hops to Englewood, CO have the same ASN (autonomous system number) - AS7843 - which is under Road Runner HoldCo LLC. And it turns out before Time Warner Cable was called Time Warner Cable, it was called <a href="https://en.wikipedia.org/wiki/Spectrum_(cable_service)#History">Road Runner</a>. Like Hunter said in class, there are lots of M&A (mergers and acquisitions).

![road runner cable]({{ site.baseurl }}/assets/und-networks/traceroute-roadrunner.png)

All of these hops have Time Warner Cable as the ISP, which makes a lot of sense. Next, the traceroute stops at an IP from Tata Communications in NYC. I'm guessing they connect in a meet-me-room before jumping to Google's network in Southport, NC. Southport right on the coast, so I think there must be some easy access to fiber cables here, but I can't find anything about it online. Finally, it hops to Mountain View and bounces around within Google's <a href="https://en.wikipedia.org/wiki/Autonomous_system_(Internet)">autonomous system</a>, which is AS15169, before it gets to its destination.

NYU's network is a little different. It seems to bounce between Teterboro, NJ and Herndon, VA before getting to Southport, NC. Both the Teterboro and Herndon hosts have Tata Communications as the ISP. However, the Teterboro location's ASN (AS32098) is listed under Transtelco Inc (not Tata Communications!). It looks like Tata Communications might be using bandwidth from [Transtelco](https://transtelco.net/carrier-services/) to extend their network.

I'm not sure why the traceroute sometimes bounces back to a previous location - for my apartment and the coffee shop it went to Englewood, CO and then back to NYC before continuing. For NYU it hopped to Teterboro, NJ and back to Herndon, VA. It seems unnecessary to do that and I'm guessing it has to do with traffic? Or possibly the infrastructure isn't there? Can router deny further travel and force the request to go back? Or that the router knows that it is somehow thinks it is faster to go the longer route? So many questions!


## beverlychou.com vs itp.beverlychou.com

I wanted to make a map for my blog (itp.beverlychou.com) but it stops getting replies from any hosts after about 7-9 hops. The traceroute from ITP and my apartment never leave NYC, and the one from the coffee shop makes a hop to Los Angeles. All of them timed out after 64 hops (the supposed diameter of the internet).

I wonder if it has to do with any protections that Github has in place. Both the traceroute from my apartment and the coffee shop never show anything besides Time Warner Cable as the ISP. The traceroute from ITP stays in NYU's network before making the last visible hop to Level 3's network. I ran a traceroute to Github.com from ITP with similar results. This makes sense since my blog is hosted by Github. It seems like Github is unresponsive or too busy to reply to traceroute requests.  

![]({{ site.baseurl }}/assets/und-networks/traceroute-mysite.jpg)

On the other hand, the traceroutes for my portfolio site (beverlychou.com) is a little more interesting. At home and the coffee shop, the traceroutes are pretty similar. It appears to start in Time Warner Cable's network in NYC before going through Zayo Bandwith's networks in Louisville, CO and Emeryville, CA. Then it ends in DreamHost's network in Brea, CA. Zayo's ASN is 0. I looked up what this means [according to the Internet Engineering Task Force (IETF)](https://tools.ietf.org/html/rfc7607), and it says it is "Reserved - May be use [sic] to identify non-routed networks". I'm not sure what that means, but I also looked up [Zayo](https://www.zayo.com/). They are a carrier neutral company that provides infrastructure to other companies, so that kind of makes sense that their ASN is 0.

The traceroute from ITP looks like it goes through the carrier hotel at 60 Hudson before it leaves NYC since the hostname at this hop is "via-60-hudson-nyc002jp01.yipes.com". I don't know why it then bounces between somewhere in Ireland and France where GTT Communications Inc is the ISP before coming back to Louisville, CO in Zayo Bandwidth's network. I looked at [GTT's wikipedia page](https://en.wikipedia.org/wiki/GTT_Communications), and they specialize in this thing called [IP transit](https://en.wikipedia.org/wiki/Internet_transit). Wikipedia defines it as "the service of allowing network traffic to cross or "transit" a computer network, usually used to connect a smaller Internet service provider (ISP) to the larger Internet". This makes sense since NYU is a smaller network trying to connect to a bigger global network. As for why they are sending the info out to Europe, I still don't understand that. Maybe that's just where their infrastructure is? They are an American company based in Virginia, so I'm not sure that is the case.

I really thought that I would see something where my blog would go to DreamHost and then Github, while my site would only go to DreamHost. That wasn't the case though. They both tried to go directly to where the sites were hosted. I clearly need to read more about how DNS works.

## Other Observations

I noticed that on all non-NYU routers (my home and the coffee shop) always had a *** on the second host it hopped to. My guess is that as my request for the website leaves my private network it goes through a firewall or that my router automatically will not reply to traceroutes because it's private. I'm not 100% sure, but I think it is some precaution to protect you from people on the outside.

## Spreadsheet of Collected Data

<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vQTUsgzzhTyGcylY6KEfLUZOLVM835t4I2Ar-psEf0eO-NAKOxKu6tCDDoNfS1fv7WKRfMKoIuf3KKt/pubhtml?widget=true&amp;headers=false"></iframe>

## Helpful Links
- [Look up Autonomous Systems](https://ipduh.com/ip/whois/as/)
- [Bulk IP Address look up](https://www.infobyip.com/ipbulklookup.php)
