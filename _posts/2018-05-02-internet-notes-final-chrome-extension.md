---
layout: post
title: Internet Notes - Final Chrome Extension
date: 2018-05-02
type: post
categories:
- Hacking the Browser
tags:
- HTML
- CSS
- Firebase
- Javascript
- Chrome Extension
- Tabs API
meta:
author:
   Beverly
---

![google]({{ site.baseurl }}/assets/hackbrowser/final-google.png)

[CLICK HERE to download the extension here!]({{ site.baseurl }}/assets/hackbrowser/w7-final-internet-notes-extension.crx) And then go to "chrome://extensions/" and drag the downloaded file into the page.

I made a Chrome extension that lets people leave anonymous notes on any website. Anyone who has the Chrome extension can see the notes. The idea is that it would be fun to randomly find little notes left by people, kind of like a digital version of writing a note in a book for someone to discover. I'm aware that because of the anonymous nature it could potentially attract trolls, but I think it'll be okay for now with ITP users.

The image above show some messages from our lovely Hacking the Browser class that they posted on google.com! Here's what it looks like when you are posting a message.

<p><div class="responsive-container"><iframe src="https://player.vimeo.com/video/267657390" width="640" height="449" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div></p>

I used Chrome's tabs, browserAction, and runtime APIs. I also used a Firebase database for the message information. In the rest of the post, I'll go over the main components of the extension.

<!--more-->

## The Manifest file

Starting with my manifest.json file, I had to get permissions for the tabs API because I needed to access the user's URL and inject CSS into the page. I needed permissions for all URLs because I wanted my extension to work on any website.

I had the scripts for Firebase and JQuery in my extension file, so those are included as well. My extension has a popup for users to input their messages, so I also have the browser action API included.

{% highlight jsonnet %}
{
  "name": "internet notes",
  "version": "1.0",
  "manifest_version": 2,
  "description": "a nice description here",

  "browser_action": {
    "default_title": "click me to add a note",
    "default_popup": "popup.html"
  },

  "background": {
    "scripts": ["jquery.js", "firebase.js", "background.js"]
  },
  "permissions": [
    "tabs",
    "<all_urls>"
  ]
}
{% endhighlight %}

## Sending Data From the Popup to the Background script to Firebase

Here's what my little popup looks like right now.

![popup window]({{ site.baseurl }}/assets/hackbrowser/final-early-stages-popup.png)

Starting with the user's input from the popup, which is a message and a timestamp, I put that info into an object and then used the runtime API to send it to the background script using "chrome.runtime.sendMessage()".

{% highlight javascript %}
//THIS SNIPPET IS FROM POPUP.JS
//get info from the popup.html window
function getInfo() {
  //get the current time
  let timestamp = new Date().getTime() / 1000;
  timeStr = convertDate(timestamp);
  //get the user's message
  userMsg = document.getElementById("userText").value;
  //make object
  let newNote = {
    time: timeStr,
    msg: userMsg
  }
  //send to background.js
  chrome.runtime.sendMessage(newNote);
}
{% endhighlight %}

The background script receives the message using "chrome.runtime.onMessage.addListener()". Following that, I am getting the current URL, creating a new object with all the data and then pushing it into my Firebase database.

{% highlight javascript %}
//THIS SNIPPET IS FROM BACKGROUND.JS
chrome.runtime.onMessage.addListener(function(data, sender, sendResponse) {
  //got time and message data
  console.log("message received!");
  currentTime = data.time;
  currentMsg = data.msg;
  //get URL of selected tab
  chrome.tabs.getSelected(null, function(tab) {
    currentURL = tab.url;
    //put all the data into a JSON
    let newData = {
      time: currentTime,
      msg: currentMsg,
      site: currentURL
    };
    //push to firebase
    var database = firebase.database();
    var ref = database.ref("test");
    ref.push(newData);
  });
{% endhighlight %}

## Getting Data from Firebase and Inserting it into Websites

Next, I needed to get the data from Firebase and then display it on the website if users had made posts on it. To do this, I queried my database using "equalTo". This returns the keys of the data, and then I was able to read the data once to get the values that are associated with those keys.  

{% highlight javascript %}
//THIS SNIPPET IS FROM BACKGROUND.JS
//query database for data that match the active URL
var ref = firebase.database().ref("test");
ref.orderByChild("site").equalTo(activeURL).on("child_added", function(snapshot) {
  keys.push(snapshot.key);
});
console.log(keys);

//get data under each key in the key array
for (let i = 0; i < keys.length; i++) {
  var refForData = firebase.database().ref("/test/" + keys[i]);
  refForData.once("value").then(function(snapshot) {
    msgToPost.push(snapshot.val());
  });
}
{% endhighlight %}

Before I can post it, I need to send this data, "msgToPost", to my content script where I will display the messages on the website. To do this, I used the tabs API's "sendMessage" to send the data to the active tab.

{% highlight javascript %}
//THIS SNIPPET IS FROM BACKGROUND.JS
//find the active tab
chrome.tabs.query({
  active: true,
  currentWindow: true
}, function(tabs) {
  //send array of msg data to content script
  chrome.tabs.sendMessage(tabs[0].id, {
    action: "postmsg",
    array: msgToPost
  }, function(response) {});
});
{% endhighlight %}

Now, I needed to run a content script to get the message to show up in the website.

{% highlight javascript %}
//THIS SNIPPET IS FROM DISPLAYMSG.JS
//get msg data from the background script
chrome.extension.onMessage.addListener(function(msg, sender, sendResponse) {
  if (msg.action == "postmsg") {
    //get the message array
    let incomingMsg = msg.array;
    //don't post anything unless there is data
    if (msg.array.length == 0) {
      // document.getElementById("allMsgs").remove();
      console.log('nothing to show!')
    } else {
      //add the div for all messages
      displaySetup();
      //loop through the message array + add to allMsgs
      for (let i = 0; i < incomingMsg.length; i++) {
        appendPost(incomingMsg[i].time, incomingMsg[i].msg);
      }
    }
  }
});
{% endhighlight %}

And that results in the messages showing up!

![itp help]({{ site.baseurl }}/assets/hackbrowser/final-itp-help.png)

Thanks to Cory and the Hacking the Browser class for a fun semester!
