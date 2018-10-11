---
layout: post
title: Webcam Chat
date: 2018-10-9
type: post
categories:
- Live Web
tags:
- Javascript
- WebRTC
- Webcam
- Web Sockets
meta:
author:
   Beverly
---

<!-- {{ site.baseurl }} -->
![gif of several users sending messages]({{ site.baseurl }}/assets/live-web/video-chat-demo.gif)

I tried out using HTML5 video and WebRTC. I've also got HTTPS running on my site now too! I made a chat where you can send images from your webcam. It works with multiple people, but it's only me and my friend Jeff in this gif.

[This reference](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Taking_still_photos) on the MDN site was a good resource and I figured out how to fix the weird resolution issue getting the video images to the canvas.

<!--more-->

### Getting HTTPS

In the server file, I added the certificates and changed it to require https. And that's basically it.

{% highlight javascript %}
//IN THE SERVER.JS FILE
var https = require('https');
var fs = require('fs');

var options = {
  key: fs.readFileSync('my-key.pem'),
  cert: fs.readFileSync('my-cert.pem')
};

var httpServer = https.createServer(options, requestHandler);
var url = require('url');
httpServer.listen(8080);
{% endhighlight %}


### HTML5 Video

So the main thing was getting the video to be the right resolution. I figured out that you need to set the height and width of the canvas after the video is able to play. I figured it out by reading about it [here](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Taking_still_photos).

{% highlight javascript %}
//IN THE SKETCH.JS FILE
let width = 300;
let height = 0;
let streaming = false;

// if video is able to play
video.addEventListener('canplay', function(ev) {
  if (!streaming) {
    // set the width and height of video and canvas the same
    height = video.videoHeight / (video.videoWidth / width);
    video.setAttribute('width', width);
    video.setAttribute('height', height);
    canvas.setAttribute('width', width);
    canvas.setAttribute('height', height);
    streaming = true;
  }
}, false);
{% endhighlight %}

Then getting the video is pretty much the same code as what we did in class.

{% highlight javascript %}
//get elements
let video = document.getElementById('myVideo');
let canvas = document.getElementById('myCanvas');
let sendPic = document.getElementById('sendPic');

// what media we want
let constraints = {
  audio: false,
  video: true
}

// get permission to get video/audio
navigator.mediaDevices.getUserMedia(constraints).then(function(stream) {
    // attach stream to video object
    video.srcObject = stream;
    // wait for stream to load enough to play
    video.onloadedmetadata = function(e) {
      //play video
      video.play();
    };
  })
  // if error, send to console
  .catch(function(err) {
    console.log(err);
  });
{% endhighlight %}

In my css, I hid the canvas and only showed the video, which is on the right side.

### Web Sockets

 There is more code on the server to receive and emit the data, but these are the important parts on the client side. To send the images, I have an event listener on the "send" button. I draw the image to the canvas and then I convert the canvas image to a data URL that I send to all the clients.

{% highlight javascript %}
//IN THE SKETCH.JS FILE
//when you click on send button
sendPic.addEventListener('click', function() {
  //get canvas context
  let context = canvas.getContext('2d');
  //when the width and height are available
  //draw the image to the canvas
  if (width && height) {
    canvas.width = width;
    canvas.height = height;
    context.drawImage(video, 0, 0, width, height);
  }
  //get the data URL & send to other clients
  let imgDataURL = canvas.toDataURL();
  socket.emit('webcamImg',imgDataURL);
});
{% endhighlight %}

When I receive the images, I create a new image element and then use "insertBefore" to add the images to the top of the chat body, which is the yellow box on my site.

{% highlight javascript %}
//IN THE SKETCH.JS FILE
socket.on('webcamImg', function(dataURL) {
  console.log("get video frame data");
  let newImg = document.createElement('img');
  newImg.src = dataURL;
  let chat = document.getElementById('chatBody');
  chat.insertBefore(newImg, chat.childNodes[0]);
});
{% endhighlight %}

### All of the Code

![bye]({{ site.baseurl }}/assets/live-web/video-chat-bye.jpg)

Thanks for reading! All the code is available [here](https://github.com/bevchou/live-web/tree/master/2018_10_9_VideoChat).
