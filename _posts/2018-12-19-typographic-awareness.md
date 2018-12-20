---
layout: post
title: Typographic Awareness
date: 2018-12-19
type: post
categories:
- Live Web
- Computational Approaches to Typography
tags:
- Finals
- Typography
- Peer.js
- Chrome Extension
meta:
author:
   Beverly
---

<!-- {{ site.baseurl }} -->

For my final, I combined my finals projects for Live Web and Computational Approaches to Typography. I made slightly different versions for each class, but I would like to combine them into one fully functional Chrome extension in the future. My original idea is [here](https://itp.beverlychou.com/online-typographic-awareness/).

## Playing with Type

![demo gif]({{ site.baseurl }}/assets/comp-typo/typo-awareness-demo.gif)

I started by writing the code to create the interactions I wanted users to have. Mainly I wanted users to mouse over blocks of text and have it look like it was rippling. Here is a basic overview on how my code works:

1. Use a [Treewalker](https://developer.mozilla.org/en-US/docs/Web/API/TreeWalker) to get all the text nodes on the page
2. Loop through all the text nodes, and put each text node into a new charGroup element.
3. Replace the inner HTML of the charGroup string into individual character elements. If one of the charGroup elements was "word" it would be replace with "<character style='display:inline-block;>w</character><character style='display:inline-block;>o</character><character style='display:inline-block;>r</character><character style='display:inline-block;>d</character>".
4. Then I replace the new charGroup element where the original text node used to be.
```
textnodes[i].parentNode.replaceChild(newNode, textnodes[i]);
```
5. Finally, after it finishes looping through all the text nodes I can manipulate the individual character elements using the [animate API](https://developer.mozilla.org/en-US/docs/Web/API/Element/animate) and the 'mousemove' event listener.

I also used the ambient light sensor to change text opacity and the background color. I think the background color change doesn't really work that well since the user needs to enable "Generic Sensor Extra Classes" in their Chrome flags. Regardless, I'm glad it worked and I liked this for a first iteration.

All the final code for the Chrome extension is [here](https://github.com/bevchou/computational-approaches-to-typography/tree/master/typo-chrome-ext-final) and you can download it [here](https://github.com/bevchou/computational-approaches-to-typography/blob/master/typo-chrome-ext-final.crx). Install the extension by going to chrome://extensions and then dragging the file into the browser. Activate the code on any website by click on the extension icon.

## Adding more users with Peer.js

![demo gif]({{ site.baseurl }}/assets/live-web/final-demo.gif)

The site is up [here](https://itp.beverlychou.com/live-web/final_v_1_website/) as long as my peer server is still running.

I was able to get Peer.js working within a Chrome extension, but then I had issues with keeping the same peer id as the user went to a new page. I think I needed to use the storage API to permanently store the peer id, but I borrowed a website from Frank De La Cruz at Columbia to show peer.js working for class.

I basically have peer.js sending the mouse and ambient light data as it is received from the other user. Users can choose their own peer id and then call other people whose peer ids they know. I wanted it to be intentional that the other user knows who they are contacting so it's not totally anonymous and creepy.

All the final code for the web version is [here](https://github.com/bevchou/live-web/tree/master/final_v_1_website).

I think this was good for a first iteration, but I'm hoping to fully combine the peer.js and chrome extension in the future. I'm also thinking about adding it to my website/blog so you can see if anyone else is also there (:


## Reference Links

- [What Web Can Do Today](https://whatwebcando.today)
- [Animate elements function in Web API](https://developer.mozilla.org/en-US/docs/Web/API/Element/animate)
- [Find and replace text characters](https://stackoverflow.com/questions/18643766/find-and-replace-specific-text-characters-across-a-document-with-js)
- [Nodes MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentNode)
- [Text elements MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Text)
- [Get elements from point (get an array of elements that are under your mouse) MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/DocumentOrShadowRoot/elementsFromPoint)
- [Get the top most element from point MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/DocumentOrShadowRoot/elementFromPoint)
- [Using the ambient light sensor](https://blog.arnellebalane.com/using-the-ambient-light-sensor-api-to-add-brightness-sensitive-dark-mode-to-my-website-82223e754630)
- [Regular expression to remove white space in text](https://stackoverflow.com/questions/22921242/remove-carriage-return-and-space-from-a-string)
- [Find all text nodes on a site](https://stackoverflow.com/questions/10730309/find-all-text-nodes-in-html-page)
