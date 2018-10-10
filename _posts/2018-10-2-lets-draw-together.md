---
layout: post
title: Let's Draw Together
date: 2018-10-2
type: post
categories:
- Live Web
tags:
- Javascript
- Web Sockets
meta:
author:
   Beverly
---
<!-- {{ site.baseurl }} -->
![gif of several users drawing]({{ site.baseurl }}/assets/live-web/draw-together-demo.gif)

Ivy and I made a simple drawing application where users can draw together using different colors when they go to the same site. We used socket.io to send the mouse position from all the users and the draw the image on everyone's screen.

<!--more-->

### About the Code

Using p5, whenever the user draws, we emit the mouse position.

{% highlight javascript %}
//IN THE SKETCH.JS FILE
function mouseDragged(){
  fill(dotColor);
  console.log('Sending: ' + mouseX +',' + mouseY);
  var data = {
    x:mouseX,
    y:mouseY
  }
  socket.emit('mouse',data);
  noStroke();
  ellipse(mouseX, mouseY, 5,5);
}
{% endhighlight %}

The server gets this data, and then sends it to all the other clients.

{% highlight javascript %}
//IN THE SERVER.JS FILE
socket.on('mouse', function(data) {
  console.log(data);
  socket.broadcast.emit('mouse', data);
});
{% endhighlight %}

And then when the clients receive the mouse data, we use it to draw the image onto the p5 canvas.

{% highlight javascript %}
socket.on('mouse', function(data) {
  noStroke();
  fill(dotColor);
  ellipse(data.x, data.y, 5, 5);
});
{% endhighlight %}

### Trying the Citizen App

I tried using the [Citizen app](https://itunes.apple.com/us/app/citizen/id1039889567?mt=8) the past few weeks, and honestly it makes me sort of anxious.

First, there is a lot of petty crime but there's also a lot serious crime that is reported through the app. NYC is a big, dense city so I guess it shouldn't be surprising that things happen in areas I frequent. Maybe ignorance is bliss and I don't need to know about every little thing?

Another thing which is interesting is that people can live stream things. This could be good because it might help to provide detailed accounts of incidents. It could also be encouraging people to be bystanders when they should be taking action to help the situation. This also might be a good way provide info that is less biased (though the comments are sort of toxic) than popular news sources. I'm not sure how I feel about this being a useful app.

This is exactly the kind of thing my parents would see and think that danger is lurking around every corner of NYC. I'm probably going to delete this from my phone because I think we have enough to stress about.
