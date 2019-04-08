---
layout: post
title: Packet Sniffing a Google Home
date: 2018-10-28
type: post
categories:
- Understanding Networks
tags:
- Wireshark
- Herbivore
- Packet Sniffing
meta:
author:
   Beverly
---

![picture of my google home mini]({{ site.baseurl }}/assets/und-networks/packetsniff-google-home.jpg)

I decided to packet sniff a Google Home Mini that my sister gave me last year for Christmas. When I told her I didn't want to use it because Google was probably collecting all our data, she was pretty upset that I didn't appreciate her gift. I briefly used it out of guilt, but eventually it creeped me out too much so I quietly stopped using it (sorry, Ann). Now using Wireshark, I hope to report that my concerns are completely valid.

<!--more-->

### Setting Up Wireshark

<!-- {{ site.baseurl }} -->

I didn't want to accidentally snoop on anyone else's data so I needed to determine the IP address of the Google Home after connecting it to the wifi. I looked at our Spectrum router's gateway where you can manage the router's settings and see all the devices that are connected. I was able to find the IP address of the Google Home there.

![ip address of google home]({{ site.baseurl }}/assets/und-networks/packetsniff-google-home-ip.png)

Then I could set the capture filter on Wireshark to only view packets that were coming or going from the Google Home.:

```
host 192.168.1.19
```

I also made a note of important IP addresses - particularly my laptop. It was helpful to change the preferences in Wireshark so you can see the names of the devices instead of a ton of IP addresses. Name resolution > check yes to resolve network (IP) addresses.

### Capturing the Packet Data

There are a couple of behaviors that I noticed while using the Google Home Mini. The device seems to communicate mainly using TCP and mDNS protocols. It occasionally uses ARP and AJP13. There are two specific instances where I noticed that the packet behavior changed significantly - 1) when my laptop has Google Chrome open and 2) when Chrome is closed. I noticed this behavior while casually watching the stream, and then decided to capture a cleaner snapshot of data. My plan was as follows.

| Time (Minutes) | Action |
| --- | ----------- |
| 0 | Google Home is on. Start Wireshark. Have Chrome open. |
| 0-3 | Browse Internet using Chrome as usual. |
| 3-6 | Stop browsing Internet using Chrome. |
| 6-9 | Ask Google Home to play music. |
| 9-12 | Close Chrome. Allow music to continue playing. |
| 12-15 | Ask Google Home to stop music. Allow for ambient sound and talking. No direct interaction. |
| 15-17 | Ask Google Home a couple really weird specific questions. |
| 17-20 | Ask Google to play music again. |

And here is a beautifully formatted Excel plot of the data captured over time by protocol.

![plot of packets capture over 20 minutes by protocol]({{ site.baseurl }}/assets/und-networks/packetsniff-plain-time-plot.png)

Here are some added notes to make it more clear what was happening in real life during this packet capture.

![plot of packets capture over 20 minutes by protocol]({{ site.baseurl }}/assets/und-networks/packetsniff-w-notes-time-plot.png)

### TCP Communication with my Laptop

When I was initially looking at the packet stream, I was really confused that my laptop and the Google Home were sending SO MANY packets to each other. I thought that the Google Home would be communicating with a Google IP address.

Essentially, for the entire time that Chrome was open on my laptop, my laptop would send two successive TCP packets and receive a TCP packet from the Google Home over and over again. Here is how the pattern of the TCP packets (and the included flags) went:

1. laptop to google home: ACK - no payload
2. laptop to google home: PSH, ACK - yes payload
3.  google home to laptop: PSH, ACK - yes payload

This pattern went on in an endless cycle until I closed Chrome. We've seen the acknowledgement (ACK) flag before since it is an important part of TCP, but the push (PSH) flag was new. Essentially, the PSH flag tells the sender that the TCP data should be sent right away and it tells the receiving host to immediately push the data to the application. Without the PSH flag, the packet may sit in a buffer and cause a delay.

The first packet is simply an acknowledgement that my laptop got the previous packet that was sent from the Google Home. It didn't have any payload attached. The second and third ones have payloads. I tried to see what data was being transmitted, but looking at the payloads didn't really tell me anything. My guess is that the packets are encrypted and broken into pieces. Wireshark indicates "TCP segment of a reassembled PDU" on many of the packets.

Once, I closed Chrome the TCP packets stopped. My laptop sent Google Home a TCP packet with a "FIN" flag to indicate it was the last packet it would send. There's some errors about duplicate acknowledgement and out-of-order packets. Then my laptop sent a "RST" flag to reset the connection. From there the TCP packets end.

Anyways, I'm not 100% sure what was being sent but based on the behavior it seems like Google is sending realtime data between Google Home and Chrome (when it's available). Is the microphone on the Google Home listening? Maybe it's waiting for us to [play content from Chrome to Google Home](https://support.google.com/googlehome/answer/7194413?hl=en)? Maybe Chrome is sending data to predict what I'll ask Google Home? Is it doing a software update? Who knows. They seem pretty vague about it, but rest assured they're making their services "better" - whatever that means.

![]({{ site.baseurl }}/assets/und-networks/packetsniff-google-home-what-they-doing-data.png)

As a paranoid person, I'd guess Google is collecting data on us. Even in the time where I have Chrome open and I'm not doing anything (3-6 min in the chart) Google Home and my laptop are sending a lot of data to each other. I'd need to packet sniff on my laptop as well to see if Chrome is sending the data it receives to an IP outside of my apartment.

### mDNS Communication / Who is 224.0.0.251?

DNS is domain name system, which converts a computer's host name to an IP address that identifies it on the Internet. mDNS is multicast-DNS, which works similarly on a smaller network (like the network in my apartment) instead of the entire Internet. mDNS and DNS are in the application layer, and both use UDP.

mDNS works by broadcasting a query to all the hosts on the local network. Then the ones with hostnames that match the query will respond to one that sent the query. mDNS is assumed to be used in a trusted network and the packets are not secure. To avoid flooding the network with traffic, it uses a lot of caching.

In terms of the Google Home, it sent a series of 2-3 mDNS packets approximately every 1.7 minutes (compare that with ~40 TCP packets per minute sent between my laptop and the Google Home when Chrome was open). This is probably because it was caching data. There are some packets which indicate a cache purge. The Google Home always sent a packet to the IP address 255.0.0.251, but never received any mDNS packets. Packets show that it is still querying and getting responses though.

![]({{ site.baseurl }}/assets/und-networks/packetsniff-mDNS-only.png)

The Google Home was able to answer all my really weird specific questions (15-17 minutes on the chart) without sending queries at the exact moment I asked the question. I think it might be continuously listening (and caching) and then continuously bringing back results. And then if it senses the hot word (because it's always listening) it can tell me the relevant answer it has cached away. I'm not quite sure, but I expected that it would send or receive packets at the moment I ask questions that are uncommon.

So who is 224.0.0.251???? It's a [multicasting IP](https://www.iana.org/assignments/multicast-addresses/multicast-addresses.xhtml). According to Wikipedia, "IP multicast is a technique for one-to-many and many-to-many real-time communication over an IP infrastructure in a network." The packets show the Google Home is talking to services called "\_googlecast.\_tcp.local" and "\_googlezone.\_tcp.local" that are also sending info to 224.0.0.251. There is info in the query response packets that include my Google Home's unique id, and I think that is how it identifies the relevant data to grab.

These packets aren't encrypted. I can see some of the metadata under "additional records". Here you can see the name of my Google Home, bc-room, and that I'm streaming music from Spotify. It's also probably possible to view more data at the unique domain for my Google Home when it's on the network? Not sure, I'd need to look while it is connected.

![]({{ site.baseurl }}/assets/und-networks/packetsniff-a-response-mdns-packet.png)

Anyways, it seems like Google other streaming products like Chromecast also use mDNS in the same way, and probably several other smart or networked devices function this way.

### Conclusions

Besides the packet sniffing, I'm not a fan of it as a product. The voice interface wasn't a smooth experience and I didn't find it helpful. It didn't introduce enough convenience in my life and the sound quality (as a speaker) is pretty bad. And besides all those things, I'm still convinced it's constantly listening and saving my data even if I can't prove what's in the TCP packets. And we shouldn't forget that they can change the software unbeknownst to all of us at any point in time. I'm not sure if it's really that big of a step to avoid using Google's smart home devices because they probably know enough about me from my usage of all their products. In any case, I feel better with the Google Home unplugged.

### Links for Reference

- [PSH and URG flags on TCP](http://packetlife.net/blog/2011/mar/2/tcp-flags-psh-and-urg/)
- [Wikipedia about TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)
- [Wikipedia about mDNS](https://en.wikipedia.org/wiki/Multicast_DNS)
- [Simple Wikipedia on DNS](https://simple.wikipedia.org/wiki/Domain_Name_System)
- [Official mDNS website from creator Stuart Cheshire](http://www.multicastdns.org/)
- [mDNS description](https://stackoverflow.com/questions/1499510/why-does-mdns-bonjour-avahi-etc-use-udp)
- [mDNS description from someone else](https://stackoverflow.com/questions/11835782/how-exactly-does-mdns-resolve-addresses)
- [what is multicast doing on 224.0.0.251](https://stackoverflow.com/questions/12483717/what-is-the-multicast-doing-on-224-0-0-251)
- [multicast IP](https://en.wikipedia.org/wiki/IP_multicast)
- [people on reddit wondering the same thing as me](https://www.reddit.com/r/Chromecast/comments/94kazy/how_exactly_can_all_chromecast_audios_in_a_group/)

Side note: [Simple English Wikipedia](https://simple.wikipedia.org) is amazing.

### Interesting Google Home related Links

- [Local Google Home API](https://github.com/rithvikvibhu/GHLocalApi)
- [More Conversation about Local API from Reddit](https://www.reddit.com/r/googlehome/comments/7qg6ef/use_the_api_on_your_google_home_to_view_things/)
