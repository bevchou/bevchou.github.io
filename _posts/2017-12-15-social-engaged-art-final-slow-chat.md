---
layout: post
title: Socially Engaged Art Final - Slow Chat
date: 2017-12-15 23:46:09.000000000 -05:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Socially Engaged Art and Digital Practice
tags:
- Heroku
- node.js
- NYU-ITP
- p5.js
- socially engaged art
- socket.io
meta:
  _edit_last: '1'
author:
   Beverly




---
<p>Throughout this class, I have been thinking about social engaged art in two main ways. The first being SEA that explores making social impact within a community through the creating situations where unlikely groups collaborate. The key thing is that everyone is gaining something valuable from the collaboration so there is equal ownership and no one feels taken advantage of. I also feel that making critical thinking about art and creative practices a part of education can break down the sentiment that "Art" is inaccessible outside of the art world. This manifested in my idea where media sources, students, and local creative practitioners would collaborate together through a class for the students to produce content that is more accessible to a mainstream population and that uplifts narratives of a community’s history and lived experiences.</p>
<p>The second way I've thought about SEA is how we might use it to examine our social behaviors that are enabled by technology. In particular, the fact that a lot of digital tools we use are claiming that they help us become more connected, while on the other end, critics claiming our obsession with devices is making us less connected. Connection in the digital space vs connection in real space? I'm starting to think that the line between those two "spaces" are becoming more ambiguous in people's minds.</p>
<p>A lot of the inspiration for this arises from my own experiences communicating with people in digital spaces - texting in particular. Some friends tell me I am awful at texting since I don't text back fast enough. Whatever - I don't feel like I need to be on demand for people via text. But this means that there really is meaning in the unspoken aspects of texting and messaging. Is a message that's longer more meaningful? If someone waits a long time to text you back, are they mad at you? What's the deal with this instant messaging power dynamic? Is it weird that texts from your mom and from people you barely know are all at the same level and context on your phone? I think other people have these questions too.</p>
<p><img class="alignnone wp-image-490" src="{{ site.baseurl }}/assets/old-wp-content/Screen-Shot-2017-12-15-at-7.02.24-PM.png" alt="" width="374" height="344" /> <img class="alignnone wp-image-491" src="{{ site.baseurl }}/assets/old-wp-content/Screen-Shot-2017-12-15-at-7.02.01-PM.png" alt="" width="373" height="300" /></p>
<p>That leads me to my final project for this class. The main question I am asking here is what happens when users interact with a piece of technology that purposefully makes it harder to communicate? And so, my concept was to build a chat application where there are two rules: 1) Users' messages must be longer than the previous sent message and 2) The reply time between messages must be longer than the previous reply time. The idea is that the reply time and the message length would approach infinity and introduce enough inconvenience for you to perhaps connect with someone in person or just stop communicating with someone altogether.</p>
<p>I have a functioning prototype that we demoed in class. <a href="https://replytime.herokuapp.com/">You can play with it here &amp; invite someone to chat with you by sending them the URL.</a> You are greeted with this at first.</p>
<p><img class="alignnone wp-image-481" src="{{ site.baseurl }}/assets/old-wp-content/Screen-Shot-2017-12-15-at-6.17.19-PM.png" alt="" width="450" height="379" /></p>
<p>Once you enter your name, you can chat with other users in the chat. In this case, our whole class was there. You can see the warnings on your screen, but others can't see them. Here is the beginning of our chat. Side note: I need to debug some of the code that checks the length/reply time of the messages, so a couple invalid messages may have slipped through if you are looking closely.</p>
<p><img class="alignnone wp-image-482" src="{{ site.baseurl }}/assets/old-wp-content/class-screenshot-1.png" alt="" width="450" height="424" /></p>
<p>It quickly escalates as people start to figure out the rules. There is ASCII art. there is posting of full articles.</p>
<p><img class="alignnone wp-image-486" src="{{ site.baseurl }}/assets/old-wp-content/class-screenshot-2.png" alt="" width="450" height="437" /><br />
<img class="alignnone wp-image-485" src="{{ site.baseurl }}/assets/old-wp-content/class-screenshot-3.png" alt="" width="450" height="461" /><br />
<img class="alignnone wp-image-484" src="{{ site.baseurl }}/assets/old-wp-content/class-screenshot-4.png" alt="" width="450" height="459" /><br />
<img class="alignnone wp-image-483" src="{{ site.baseurl }}/assets/old-wp-content/class-screenshot-5.png" alt="" width="450" height="455" /></p>
<p>This experiment with the class shows how the messages begin to lose their meaning as we are trying to fulfill the rules or test the limits of the system. I would like to see this in the context of two people trying in earnest to communicate. For now, users choose to go to my site and use the chat. I am curious to see this piece in other spaces. Maybe setting up two computers in an installation? Get more people online to use it?</p>
<p>I originally wanted it to be set up so that you could generate private URLs that you would send to the people/person you wanted to chat with, but because of the limitation of my programming skills I only made one chatroom. Also, for this prototype the file server is ephemeral (I am using a free server from Heroku), which means the messages will disappear every so often or when the Heroku server is sleeping. I would like to change this later, but for now, it works to get the point across.</p>
