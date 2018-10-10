---
layout: post
title: Color Chat
date: 2018-09-18
type: post
categories:
- Live Web
tags:
- Javascript
meta:
author:
   Beverly
---
![gif of several users sending messages and changing the background color]({{ site.baseurl }}/assets/live-web/color-chat-example-video.gif)

I wanted to make a simple chat where users can change the color of the chat box by entering in hex colors. I think colors can convey a lot of emotion and it's an interesting way to communicate without words. I wanted to find a nicer way to have users select their color, but for now it's tailored around the ease of working with CSS.

<!--more-->

I have some error messages that show up when you don't enter your color in the correct hexidecimal format.

![]({{ site.baseurl }}/assets/live-web/color-chat-error-message.png)

~~I'm not sure how to make my server run forever - it seems to close whenever I log out of my digital ocean droplet.~~

UPDATE: I've learned how to run the node server forever. You use [FOREVER](https://www.npmjs.com/package/forever). However, I don't have this site up indefinitely and I'll need to start it up via terminal if I need to demo it.

The important bit of the code is the part that is sending data between the client and the server. The server side is pretty simple. When a client is connected to the server and the server receives a message with a color, it emits the color to all the other clients.

{% highlight javascript %}
//IN THE SERVER.JS FILE
//when a client connects
io.sockets.on('connection', function (socket) {
		console.log("We have a new client: " + socket.id);

    //when receiving a color from someone
		socket.on('colorMessage', function(data) {
			console.log("Received: 'colorMessage' " + data);
			// Send it to all of the clients
			socket.broadcast.emit('colorMessage', data);
		});

    //let us know when client has left
		socket.on('disconnect', function() {
			console.log("Client has disconnected " + socket.id);
		});
	}
);
{% endhighlight %}

On the client side, there's more code. First, is the code that is getting the message from the user. And then sending it to the server. When the user hits enter, it checks if anything was entered and if the entry was actually a hex value. If the message is a valid hex color, I'll change the background color of the chat as well as the text color so that it contrasts with the background. Then I'll append the message to the chat body. Finally, I'll emit the a message that includes the username, color, and text color to everyone as a comma separated string.

{% highlight javascript %}
//IN THE CLIENT SIDE CODE - SKETCH.JS
//get the color
getColor.addEventListener('keyup', function(e) {
  event.preventDefault();
  if (event.keyCode === 13) {
    if (getColor.value == "") {
      //cannot send an empty string
      console.log("you must enter a color");
    } else {
      //check if color is hex
      if (isHex(getColor.value)) {
        myColor = getColor.value;
        //change the chat body color
        chatBody.style.backgroundColor = "#" + myColor;
        //change text to contrast the body color
        let textColor = newTextColor("#" + myColor);
        chatBody.style.color = textColor;
        //send data thru websocket
        let data = username + "," + myColor + "," + textColor;
        sendmessage(data);
        //display your message on the site
        let message = "<p>" + username + ": #" + myColor + "</p>";
        chatBody.innerHTML += message;
        //clear the input
        getColor.value = "";
      } else {
        console.log("you must enter a hex value");
        let errMessage = "<p>You must enter a hexadecimal color.</p>";
        chatBody.innerHTML += errMessage;
      }
    }
  }
});
}

var sendmessage = function(message) {
  console.log("colorMessage: " + message);
  socket.emit('colorMessage', message);
};
{% endhighlight %}

In order for the client to receive colors from other users, I needed to parse the user and color data into an array. From there, I can split the array into variables and use javascript to add the message to the chat body and update the website's styling.

{% highlight javascript %}
//IN THE CLIENT SIDE CODE - SKETCH.JS
//when you receive a color from other clients
socket.on('colorMessage', function(data) {
  console.log(data);
  //split the data into an array [name, color]
  let dataArray = data.split(',');
  let name = dataArray[0];
  let color = dataArray[1];
  let txtColor = dataArray[2];
  //change the chat body color
  chatBody.style.backgroundColor = "#" + color;
  //change text to contrast the body color
  chatBody.style.color = txtColor;
  //add message text to site
  let message = "<p>" + name + ": #" + color + "</p>";
  document.getElementById('chatBody').innerHTML += message;
});
{% endhighlight %}

All the code is available [here](https://github.com/bevchou/live-web/tree/master/2018_9_17_NodeJsColorChat).
