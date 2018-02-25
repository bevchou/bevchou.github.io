---
layout: post
title: ICM Final - Webcam Self-Portraits
date: 2017-11-28 03:57:44.000000000 -05:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- ICM
tags:
- clmtrackr
- DOM
- Final
- Flickr API
- ICM
- NYU-ITP
- p5.js
- webcam
meta:
  _edit_last: '1'
author:
   Beverly
  
  
  
  
---
<p><a href="https://beverlychou.com/ICM/webcamSelfPortraits/">CLICK HERE TO SEE &amp; PLAY</a></p>
<p><a href="https://beverlychou.com/ICM/webcamSelfPortraits/"><img class="alignnone wp-image-413" src="{{ site.baseurl }}/assets/old-wp-content/Screen-Shot-2017-11-27-at-11.21.03-PM.png" alt="" width="465" height="372" /></a></p>
<p>Plz excuse the dead look in my eyes. It's finals. Here are my questions for the class.</p>
<ol>
<li>How is interface of this website helping or hindering you from using it?</li>
<li>In what ways do you feel this does or doesn't capture your personality/identity?</li>
<li>What would you do with the photos you save from this?</li>
<li>How could this be more engaging and exciting for you?</li>
</ol>
<p><!--more--></p>
<p>I was inspired by snapchat filters and how they change our perception of ourselves. This was my initial idea.</p>
<p><img class="alignnone wp-image-409" src="{{ site.baseurl }}/assets/old-wp-content/Screen-Shot-2017-11-25-at-10.08.20-PM.png" alt="" width="417" height="312" /></p>
<p>This morphed a little bit, especially after the feedback from the project proposal class and also from the playtesting class. I also did some research on the history of self-portraits (the original selfies). I found that self portraits resonated with me the most when artists were vulnerable in using their own image to express different facets of how they view themselves. It is a way for us to see stories about their identities and feelings in a specific time, place, and society.</p>
<p>My final concept is about users creating a self-portrait through the webcam by answering questions about themselves. Using inputs from the user, I queried images using the Flickr API. The images will swirl around you to create the filter.</p>
<p>To accomplish this, I started by running the p5 webcam image with <a href="https://github.com/auduno/clmtrackr/">clmtrackr</a>. Here is the initial code. In this sketch, I created ellipse at each point from the array that is returned by clmtrackr when it detects a face.</p>
<p><img class="alignnone wp-image-416" src="{{ site.baseurl }}/assets/old-wp-content/Screen-Shot-2017-11-14-at-3.25.44-AM.png" alt="" width="114" height="158" /></p>
<p><script src="https://gist.github.com/bevchou/6f971c50029a7dba942373be66ce6122.js"></script></p>
<p>Next, I figured out how to get the DOM elements working. I needed three input fields where users would answer the questions "who are you?", "what do you like?", and "Describe yourself." For the latter two questions, I wanted to have the input fields continuously drop down as the user entered more answers. I tried to accomplish this by creating new input fields every time the user entered something. This ended up creating a duplicates when I pushed to my array that was holding the user's inputs. The more important thing I discovered in this process was that the .changed() function does not simply run one time. For instance, the callback for something like "input.changed(callback);" ended up running somewhere between 70-200 times when I hit enter - I checked it with a counter in the code.</p>
<p>I debugged this in a separate sketch. The code is below. To keep the callback from running more than once, I added "return false;" at the end. I ended up cutting down on unnecessary inputs by deleting the old input field, replacing it with a &lt;p&gt; element of the user's input, and then creating a new input field below that.</p>
<p><script src="https://gist.github.com/bevchou/7447f5a98f41fe821aa8253bf5238527.js"></script></p>
<p>The next component I needed to work with was the <a href="https://www.flickr.com/services/api/">Flickr API</a>. I used <a href="https://www.flickr.com/services/api/flickr.photos.search.html">flickr.photos.search</a> to query the user inputs either as text for the "noun" inputs (what do you like?) or as tags for the "adjective" inputs (describe yourself). In the code, I put loadJSON() in the callback function for the "input.changed();" components so the sketch could load a new JSON response every time the user entered something new. Then, in the loadJSON()'s callback function, I pushed images into an "Imgcloud" object. This happens each time the user enters something, so the "photoArray" is holding Imgcloud objects of all the photos from Flickr as well as their position info.</p>
<p><script src="https://gist.github.com/bevchou/08c8adc16a4c8f7bd4070557a9cd907a.js"></script></p>
<p>Another big issue I ran into was when to use <a href="https://p5js.org/reference/#/p5/loadImage">loadImage()</a> or <a href="https://p5js.org/reference/#/p5/createImg">createImg()</a>. When I attempted to use the save button, I got an error that my canvas was tainted!!<br />
<img class="alignnone size-full wp-image-418" src="{{ site.baseurl }}/assets/old-wp-content/Screen-Shot-2017-11-26-at-2.17.15-AM.png" alt="" width="336" height="89" /><br />
I was under the impression that because I was loading images from URLs that were not local files, I needed to put them in my sketch as DOM elements using createImg(). THIS IS NOT THE CASE. To make images as p5 elements instead of &lt;img&gt; elements, you need to use loadImage(). To summarize, loadImage() = p5 elements and createImg() = DOM elements that are not a part of your canvas.</p>
<p>Finally, the Imgcloud object specified the movement of all the images. I referenced Dan Shiffman's <a href="https://p5js.org/examples/math-polartocartesian.html">PolarToCartesian example</a> to figure out how to move the images in a circles instead of in lines. Here is how I coded the Imgcloud object.</p>
<p><script src="https://gist.github.com/bevchou/115593a395f8f65bc3cb49c55940f794.js"></script></p>
<p>Full code is available on my Github repository for this project - <a href="https://github.com/bevchou/webcamSelfPortraits">click here</a> to see! Here is a video demo.</p>
<p><iframe src="https://player.vimeo.com/video/244794385" width="601" height="470" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>Thank you for reading this far and thank you, Mimi!</p>
<p>&nbsp;</p>
