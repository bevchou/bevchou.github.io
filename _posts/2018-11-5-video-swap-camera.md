---
layout: post
title: Video Swap Camera
date: 2018-11-5
type: post
categories:
- Live Web
tags:
- Javascript
- mediaRecorder
- Web Sockets
- nedb
meta:
author:
   Beverly
---

<!-- {{ site.baseurl }} -->

![demo gif]({{ site.baseurl }}/assets/live-web/media-recorder-demo.gif)

I modified my midterm project so that it can record videos instead of taking photos. I used the [mediaRecorder API](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream_Recording_API) to accomplish this. So now when you take a short video, it'll return with a video clip randomly selected the database of video clips collected from people using the site. The API is only supported by Firefox and Chrome right now, so unfortunately this doesn't work on Safari or mobile.

<!--more-->

### Saving the videos

Now when the user clicks on the capture button, an event listener runs a function I wrote called "getVideoClip". In the function, I am getting pieces of the video stream when it becomes available (which is when the user clicks the capture button and the 'dataavailable' event gets triggered) and pushing into an array called chunks. I've set the 'stop' function to run after four sections. Then in the stop function, I create a [blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob) that contains the video data. Finally, I send the blob to the server where it stores the video file. The way the server handles the videos is the same as how my midterm project handled images.

{% highlight javascript %}
//IN THE SKETCH.JS FILE
function getVideoClip() {
  let chunks = [];
  let mediaRecorder = new MediaRecorder(myStream);
  console.log('recording a clip')

  //when recording is done
  mediaRecorder.addEventListener('stop', function(e) {
    console.log('stop');

    //create blob video
    let blob = new Blob(chunks, {
      'type': 'video/webm'
    });

    //put into an object
    let currentTime = Date.now();
    let blobObject = {
      filename: "vid_" + currentTime + ".webm",
      blobData: blob,
      time: currentTime
    }

    //send object to server
    socket.emit('videoBlob', blobObject);
  });

  //put data chunks into array
  mediaRecorder.addEventListener('dataavailable', function(e) {
    console.log('data available');
    chunks.push(e.data);
  });

  mediaRecorder.start();

  //record only 4 seconds
  setTimeout(function() {
    mediaRecorder.stop();
  }, 4000);

}
{% endhighlight %}


### All of the Code

Thanks for reading! All the code is available [here](https://github.com/bevchou/live-web/tree/master/2018_11_6_MediaRecorder).
