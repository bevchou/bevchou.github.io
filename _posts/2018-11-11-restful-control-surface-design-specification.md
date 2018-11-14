---
layout: post
title: RESTful Control Surface Design - Specification
date: 2018-11-11
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

Alden and I are working on a control interface for people to [VJ](https://en.wikipedia.org/wiki/VJing). We surveyed a couple ITPers on the floor about what makes a good VJ set. People liked when:

- Visuals reflect the mood and emotional content of the music
- Timing matches the music
- You warn people if you're gonna do a strobe effect
- There is a dynamic arc or storyline to the visuals

## Features and System Diagram

Given our restraints, we knew that timing might be an issue since using REST might not provide instantaneous feedback needed for syncing up with music. Either way, we're still doing it. In our spec, we would like to have the following options for the controller that will output to visuals (in a browser) that can be projected or shown on a screen. These are the user inputs we'd like to have on the controller.

- gif mode (on/off)
  - keyword (text input)
- abstract visual mode (on/off)
  - movement speed (range)
  - foreground color (HSL range)
  - background color (HSL range)
  - shapes/patterns (set of options)
    - rect, circle, triangle, squiggle, arc

We want the clients to communicate according to this system diagram. We are planning on using the Giphy API to pull content for the "gif mode".

![img of system diagram]({{ site.baseurl }}/assets/und-networks/REST-system-diagram-for-VJ.jpg)

~~Either a physical or digital interface will work for the controller (:~~

Update: Alden and I will be designing the control interface for the VJ visuals. Ellen and Ridwan will be designing the output visuals. Documentation on our RESTful API is available here now.

## The RESTful API

We've determined the REST API and the specific GET or POST requests that will be made by the clients.

### POST Requests

**Visualization Mode**

```
POST /mode/{value}
```
value: 0 to turn off, 1 for gif mode, 2 for abstract visual mode

**Gif Mode Keyword**

```
POST /gifword/{string}
```
string: keyword that describes desired gif

**Abstract Visual Movement Speed**

```
POST /speed/{value}
```
value: choose from range 40-180 bpm to match music speed

**Abstract Visual Foreground and Background Colors**

```
POST /foreground?h={range}&s={range}&l={range}
POST /background?h={range}&s={range}&l={range}
```
"h" value: choose from range 0-360 for hue
"s" value: choose from range 0-100 for saturation
"l" value: choose from range 0-100 for lightness

**Abstract Visual Shapes**

```
POST /shapes?triangle={bool}&circle={bool}&square={bool}&squiggle={bool}&arc={bool}
```
bool: 0 to turn off or 1 to turn on shape visibility. Bool values for each shape are independent of each other.


### GET Requests

**Current State**

Use this to request the current status of the system.  

```
GET /state/
```

will return the following:

```
{
  "mode": {0, 1, 2},
  "gifword": {string},
  "gifurl": {URL},
  "speed": {40-180},
  "foreground": {
    "h": {0-360},
    "s": {0-100},
    "l": {0-100}
  },
  "background": {
    "h": {0-360},
    "s": {0-100},
    "l": {0-100}
  },
  "shapes": {
    "triangle": {bool},
    "ellipse": {bool},
    "square": {bool},
    "squiggle": {bool},
    "arc": {bool}
  }
  "errors":{err}
}
```

**Giphy URL**

Use this to request the current gif URL so the control interface can display the gif that comes back from the Giphy server.

```
GET /gifurl/
```

will return the following:

```
{
  "gifurl": {URL},
  "errors": {err}
}
```
