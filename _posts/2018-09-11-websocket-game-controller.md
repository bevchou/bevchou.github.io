---
layout: post
title: Websocket Game Controller
date: 2018-09-11
type: post
categories:
- Understanding Networks
tags:
- WiFi
- ESP8266
- TCP
- Controller
meta:
author:
   Beverly
---

![gif of controller]({{ site.baseurl }}/assets/und-networks/websocket-controller-final-gif.gif)

I used the Feather Huzzah ESP8266 board to create my game controller. Here is an overview of what happens when using the controller.

1. Controller will connect to the itpsandbox WiFi network.
2. User hits a button to activate the connection to the server.
3. The LED inside the button will light up when the controller is connected to the server.
4. Rotary encoder dials on the top and side let the user scroll their paddle up/down and left/right.
5. When you're done playing the game, you can hit the button again to disconnect from the server and the LED will turn off.

Read more for a more detailed breakdown of the code.

<!--more-->

## Design/Build Process

When designing the controller, I tried to take advantage of materials I already had, and also I wanted to make something that was hand held. I initially had the idea to have dials that the user would rotate like in this sketch.

![sketch 1]({{ site.baseurl }}/assets/und-networks/websocket-controller-sketch1.jpg)

I had a lot of trouble securing the rotary encoders during construction. When you pushed too hard on the dials, it would bend and wobble around. Unfortunately, I forgot to photograph the first enclosure I made ): Anyways, this wasn't great for giving the user reliable control when playing the game, so I panel mounted the dials instead.

![sketch 2]({{ site.baseurl }}/assets/und-networks/websocket-controller-sketch2.jpg)

I had my breadboard set up like this. At one point, I spent an hour figuring out why my rotary encoders + buttons weren't working. I had even moved everything to an Arduino Uno to make sure it was all working (it was), only to realize that I had never connected my ESP8266 board to ground ))))):

![breadboard]({{ site.baseurl }}/assets/und-networks/websocket-controller-breadboard.jpg)

With the power/ground issue solved, everything was working well.

<p><div class="responsive-container"><iframe src="https://player.vimeo.com/video/289219307" width="640" height="1138" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div></p>

Finally, I moved things inside my enclosure. You can see the discarded first attempts in the background.

![internals]({{ site.baseurl }}/assets/und-networks/websocket-controller-inside-enclosure.jpg)

Here's the finished controller!

![sketch 1]({{ site.baseurl }}/assets/und-networks/websocket-controller-final.jpg)

## Connecting to the Wifi Network

I used the ESP8266WiFi.h library, but it is similar to the wifi101.h library. The first part of the code deals with connecting to the wifi network. When the device is connected, its IP address will print to the serial monitor.  

{% highlight javascript %}
void setup() {
  Serial.begin(9600);
  Serial.setTimeout(10);
  socket.setTimeout(10);

  // connect to the router
  WiFi.begin(ssid, password);
  Serial.print("Connecting to ");  
  Serial.println(ssid);
  // wait for connection to network access point:
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  // when connected to access point, acknowledge it:
  Serial.println("");
  Serial.println("WiFi connected");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP()); // print device's IP address
}
{% endhighlight %}

## Connecting to the Server

Next, I have some code that allows the user to connect and disconnect from the server that is hosting the game when they press a button. It sends 'x' to disconnect or it runs the "login()" function to connect.

{% highlight javascript %}
//within loop function
//log into the game if login button is pressed
//log out if the button is pressed again
 int loginButtonState = digitalRead(loginButton);
 if (loginButtonState == LOW && loginButtonState != loginButtonStatePrev) {
   Serial.println("button pressed");
   if (socket.connected() == false) {
     Serial.println("logging in");
     login();
   } else {
     Serial.println("logging out");
     socket.print('x');
   }
 }
 loginButtonStatePrev = loginButtonState;
{% endhighlight %}

Here is the login function that is connecting my device (the client) to the server and saying hello. The device will try to keep connecting until it is successful.

{% highlight javascript %}
//separate function outside of loop or setup
boolean login() {
  socket.connect(host, port);   // attempt to connect

  while (!socket.connected()) { // While not connected, try again
    delay(1000);
    if (socket.connected()) {   // if you connected,
      socket.println("hello");  // say hello to the server
    } else {
      // if not connected, try again:
      Serial.println("connection failed, trying again");
      socket.connect(host, port);
    }
  }
}
{% endhighlight %}

And when the device has successfully connected to the server, it will print any messages sent to the client from the server.

{% highlight javascript %}
// in the loop function
  while (socket.available()) {
    Serial.print("Got something");
    String input = socket.readString();
    Serial.print(input);
  }
{% endhighlight %}

## Tangible Controls

I used the "encoder.h" library to get inputs from my rotary encoder. I'm only showing the code for one encoder. I used a modulo function, so it only sends a signal when the encoder has been moved by more than a value of 4. This helps to make it more reliable since rotary encoders can be noisy.

{% highlight javascript %}
//initializing the encoder (outside of loop and setup)
Encoder upDownEnc(4, 5);
long upDownEncPrevPos = -999;

//up-down movement encoder in the loop function
  long upDownEncNewPos = upDownEnc.read();
  //if the encoder position changes
  if (upDownEncNewPos != upDownEncPrevPos) {
    //and it is increasing, move up
    if (upDownEncNewPos > upDownEncPrevPos && upDownEncNewPos % 4 == 0) {
      socket.print('u');
      Serial.println("up");
      delay(encoderDelay);
      //and it is decreasing, move down
    } else if (upDownEncNewPos < upDownEncPrevPos && upDownEncNewPos % 4 == 0) {
      socket.print('d');
      Serial.println("down");
      delay(encoderDelay);
    }
    upDownEncPrevPos = upDownEncNewPos;
  }
{% endhighlight %}

## Full Code

[Click here for the whole sketch.](https://gist.github.com/bevchou/1aedf7938a7c4e9e1da9b3281ab188dd)
