---
layout: post
title: Clients and RESTful API Servers for VJ Machine and Mood Jukebox
date: 2018-12-4
type: post
categories:
- Understanding Networks
tags:
- REST API
- HTTP Requests
meta:
author:
   Beverly
---

![vj demo](/assets/und-networks/vj-demo.gif)

For the VJ machine, [Ellen](https://ellennickles.com/itpblog/?category=Understanding%20Networks) and [Ridwan](https://www.ridwanmadon.com/blog/category/UnderstandingNetworks) built the API server and the screen output. Their code is on [Ellen's repo](https://github.com/ellennickles/understanding-networks/tree/master/RESTful_project/super-cool-vj-machine). Alden and I built the controller interface. Basically the controller sends POST requests to the server which is storing info on the state of the VJ machine. Then the screen output is constantly pulling with GET requests to update the visuals. Our code for the VJ machine is [here](https://github.com/miamiww/RESTfulStuff/tree/master/VJInterface).

<!-- {{ site.baseurl }} -->
![vj interface](/assets/und-networks/vj-interface.png)

We also worked with [Vidia](http://blog.vidianindhita.com/category/itp-fall-2018/understanding-networks/) and [Lucas](http://chung.work/blog/understanding-networks/) on their Mood Jukebox. Their API is available on [Vidia's repo](https://github.com/vidianindhita/mood-jukebox-api). We built their Jukebox website which functions both as the controller and the output client.

![mood jukebox](/assets/und-networks/mood-jukebox.png)

The jukebox sends a GET to get a song based on the mood and receives a reply with a song that is determined by the API server. Then the site will send a POST request to add the new song to the playlist. The jukebox site is pulling from the server using GET requests to keep the playlist updated and to determine if the jukebox state is in play mode. To change the state to play music, the site makes a PUT request when the user hits the play button, which returns the first song in the playlist. All the songs (sung by Lucas) were served from the sever so we didn't need to worry querying another source for music.

I'll go over some of the main things we ran into while working on this project.

## CORS

One of the biggest issues that we ran across while making requests to the server was cross-origin resource sharing aka [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS). Ellen and Alden did a lot of the problem solving around this (thank u! <3), and the reason we had this issue is because while the API server and the p5 visual outputs were on the same domain, the controller was on a different one. I also ran into issues while testing when they were on different ports, but the same domain. CORS tries to block requests from injecting potentially malicious javascript in to your browser. [This article](https://medium.com/@baphemot/understanding-cors-18ad6b478e2b) and [this one](https://medium.com/netscape/hacking-it-out-when-cors-wont-let-you-be-great-35f6206cc646) have a good explanations. The solution Ellen used for the VJ API is to add the [CORS node.js package](https://www.npmjs.com/package/cors) that works with Express. You "npm install cors" and then you add this code to your server.

{% highlight javascript %}
//IN THE SERVER.JS FILE
var cors = require('cors');
server.use(cors());
{% endhighlight %}

When I was working with the Jukebox, I was unable to change the code on the server side, so I used a workaround called [CORS Anywhere](https://github.com/Rob--W/cors-anywhere). I used https://cors-anywhere.herokuapp.com/ as a proxy that adds headers to the request so it doesn't trigger CORS. For all the requests you make, you put the CORS Anywhere URL before the URL of your server.

```
//make a request to
 https://cors-anywhere.herokuapp.com/http://1.1.1.1.1:8000/mydata/is/here

```

## Axios - Easiest way to make HTTP requests?

I originally started by using the [XMLHttpRequest API](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest), which worked but was not very concise or easy to understand for other people. I also thought about trying [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch), but it's in an experimental state according to MDN, so I didn't want to use it.

Alden (& also Anthony) told me to use [Axios](https://www.npmjs.com/package/axios), which comes as a node.js package, but we  used the javascript library using a CDN link. Their documentation is pretty clear and made it easy to understand what was happening in our code. Here's a snippet where I'm mkaing a POST request to the Jukebox playlist.

{% highlight javascript %}
//IN THE CLIENT JS CODE
axios({
  method: 'post',
  url: reqUrl + "/api/playlist",
  data: {
    title: newSong.title,
    artist: newSong.artist,
    mood: newSong.mood,
    genre: newSong.genre,
    url: newSong.url
  }
})
{% endhighlight %}

And here is a GET request. Nice & easy!

{% highlight javascript %}
//IN THE CLIENT JS CODE
axios({
    method: 'get',
    url: reqUrl + '/api/player/currently-playing',
  })
  .then(function(response) {
    let song = response.data;
    //do stuff with song data here
  }
})
{% endhighlight %}

## Hiding your API key + credentials

I was really confused when I couldn't get Ellen and Ridwan's VJ server code to run on my computer while I was testing it and it kept through errors about missing files. It's because Ellen is smart and didn't accidentally make her Giphy API key publicly available. You only need .gitignore and a separate file. In the server side, you need to require the file that holds your ~secret~ info. [This is a quick guide](http://c-ro.github.io/blog/node/github/2016/02/12/Hide-API-Keys-for-Github-Node.html) that helps.

{% highlight javascript %}
//IN THE SERVER.JS FILE
//the file with your secrets in your directory that also has server.js
var config = require('./config.js');

//get your API key without exposing it
var gifAPIKey = config.apikey;
{% endhighlight %}

Within the config file you would have:

{% highlight javascript %}
//IN THE CONFIG.JS FILE
apikey = "this-is-my-api-key";

  module.exports = {
    apikey
  }
{% endhighlight %}

And make a  .gitignore file that lists any files you want to hide. For instance:

```
.DS_Store
node_modules/
config.js

```
