---
layout: post
title: Midterm Camera
date: 2018-10-24
type: post
categories:
- Live Web
tags:
- Javascript
- WebRTC
- Mobile
- Web Sockets
meta:
author:
   Beverly
---

<!-- {{ site.baseurl }} -->

![demo gif]({{ site.baseurl }}/assets/live-web/midterm-camera-demo-clip.gif)

I switched my original idea to making a camera that captures your image and then shows you a randomly selected image from the database of all photos taken by other users. I thought it would be fun to surprise users with unexpected images. It could be a cool way to see what is happening in the lives of others with little context or information. Photos could come from anywhere at any time. I designed it to work on either a laptop or a phone. I think it's better on the phone since you can choose between the selfie or external facing camera. Some new things I dealt with were saving images using the file system and using nedb database to keep track of the info I was collecting.

<!--more-->

![user mode]({{ site.baseurl }}/assets/live-web/midterm-user-camera.png)
![external mode]({{ site.baseurl }}/assets/live-web/midterm-external-camera.png)

I actually did build my idea from my previous post - the image clock - but it actually ended up being sort of difficult to demo since there were not many photos stored in my database. Essentially, if any images were captured at a specific second of the day, it would show up on the site. Otherwise, you would only see a camera that doesn't seem to do anything. It's definitely a slow gratification thing. The mostly finished code for it is [here](https://github.com/bevchou/live-web/tree/master/2018_10_23_Midterm).

### Saving the images

To save the images, I needed the client side to get the image's data URL and then use socket.io to send it to the server. I used the epoch time to differentiate the image file names.

{% highlight javascript %}
//IN THE SKETCH.JS FILE
//when the user hits the capture button
captureImg.addEventListener('click', function() {
      //get the data URL & time
      let context = canvas.getContext('2d');
      let imgDataURL = canvas.toDataURL();
      let currentTime = currentDate.getTime();
      //create object to send to server
      let imgObject = {
        filename: "img\_" + currentTime + ".jpg",
        dataURL: imgDataURL,
        epochTime: currentTime,
      };
      // console.log(imgObject);
      //send object
      socket.emit('webcamImg', imgObject);
  });
{% endhighlight %}

Once the data was received by the server, I could use the file system to save it. I converted the image URL into a jpg and then saved the jpg to a folder called "imgs".

{% highlight javascript %}
//IN THE SERVER.JS FILE
// whens someone sends a video frame
  socket.on('webcamImg', function(data) {
    console.log('got img: ' + data.filename);
    let dataURL = data.dataURL;
    //convert data URL to img
    let searchFor = "data:image/jpeg;base64,";
    let strippedImage = dataURL.slice(dataURL.indexOf(searchFor) + searchFor.length);
    let binaryImage = new Buffer(strippedImage, 'base64');
    //write file
    fs.writeFileSync("/imgs/" + data.filename, binaryImage);
    });
{% endhighlight %}

### Using nedb

In addition to saving the image, I also added an object with the file path and timestamp to the database every time the server received new image data through socket.io.

{% highlight javascript %}
//IN THE SERVER.JS FILE
//create an object to store in the database
let objectToDb = {
    filename: "/imgs/" + data.filename,
    epochTime: data.epochTime,
};
//insert the object into the database
db.insert(objectToDb, function(err, newDocs) {
  if (err != null) {
    console.log("err:" + err);
    console.log("newDocs: " + newDocs);
  }
});
{% endhighlight %}

Then I get the entire database, which returns an array of objects. I randomly select an image and send it back to the client.

{% highlight javascript %}
//IN THE SERVER.JS FILE
db.find({}, function(err, docs) {
  //find the total number of images & pick one at random
  let totalImgs = docs.length;
  let index = getRndInteger(0, totalImgs - 1);
  //send the file path of random img to client
  console.log("sending img: " + docs[index].filename);
  socket.emit('returnImg', docs[index]);
});
{% endhighlight %}

When the client receives the image, I change the image source to the new file path and then show the image and hide the video. I have some similar code to manage what the user sees. I hid the "capture" button when the client is viewing an image, and then made it reappear when they return back to the camera mode.

{% highlight javascript %}
//IN THE SKETCH.JS FILE
socket.on('returnImg', function(data) {
  showImg.src = data.filename;
  showImg.style.visibility = "visible";
  video.style.visibility = "hidden";
});
{% endhighlight %}

### All of the Code

Thanks for reading! All the code is available [here](https://github.com/bevchou/live-web/tree/master/2018_10_23_Midterm_Camera).

### Nice References

If you're interested in how I was able to manage changing the camera on mobile, [the doc for getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia) is helpful. This is a great doc on how to manage [time objects.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date).
