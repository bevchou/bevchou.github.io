---
layout: post
title: Sensor Report - Magnetic Contact Switch / Reed Switch
date: 2018-02-20 19:12:50.000000000 -05:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Tangible Interaction
tags:
- Magnetic Contact Switch
- Reed Switch
- Sensor Report
- Tangible Interaction
meta:
  _edit_last: '1'
author:
   Beverly




---
<p><strong>Description</strong><br />
Many of the magnetic contact switches I found are composed of two pieces. One side has a magnet in it and another side has a reed sensor in it. The side with the magnet will not have any wires coming out, but the sensor side will have two wires. Normally they are enclosed in a plastic housing that allows users to mount them with screws or press fit into a hole. The side with the wires and the reed switch is the part that will hook up to your microcontroller.</p>
<img class="wp-image-621" src="{{ site.baseurl }}/assets/old-wp-content/Adafruit-Magnetic-Contact-Switch.jpg" height="350" alt="" />
###### Magnetic door contact switch (from Adafruit)

<img class="wp-image-620" src="{{ site.baseurl }}/assets/old-wp-content/amazoncontactswitch.jpg"  height="350" alt="" />
###### Magnetic window contact switch (from Amazon)
<br>
<!--more-->
<p><strong>How does a typical reed switch work?</strong></p>
<img class="wp-image-623" src="{{ site.baseurl }}/assets/old-wp-content/reed-switch.jpg" alt="" height="350"/>
###### A reed switch without the enclosure

<p>Inside the switch’s glass casing there are two thin pieces of conductive, magnetized material that are parallel to each other. When the switch is near a magnetic field, the two magnetized contacts will react. Reed switches come in two different varieties which determine how they behave and will affect how you set up your code.</p>
<ul>
<li> Normally open (NO)
<ul>
<li>By itself the switch is open</li>
<li>When the switch is near a magnet, the switch closes</li>
</ul>
</li>
<li>Normally closed (NC)
<ul>
<li>By itself the switch is closed</li>
<li>When the switch is near a magnet, the switch opens</li>
</ul>
</li>
</ul>
<p>There is likely a point when the magnet is not close enough to fully activate the switch and not far enough to deactivate the switch. This will probably create some noise in your sensor readings so depending on how you use the switch, you may need to integrate debouncing into your code to get the reading you want.</p>
<p><strong>Example Use Case Scenarios</strong><br />
Most of these switches that you find readily available on Adafruit or Amazon are intended for security purposes to check if doors and windows are fully closed. However, you can use them for many other applications. Essentially, these switches are useful for when you have two items/surfaces that can move freely, but you want to sense when they touch or come near each other. Here are some use cases in everyday products:</p>
<ul>
<li>Knowing when your laptop lid is closed or not</li>
<li>Sensing when an electronic device has been placed into a docking station</li>
<li>Determining whether your refrigerator door is shut</li>
<li>Sensing water/fluid levels</li>
<li>Measuring distance in an odometer</li>
</ul>
<p>Here are some free ideas:</p>
<ul>
<li>Count the number of rotations of an object by putting a magnet on the edge of the spinning piece and putting a reed switch in a fixed position near it</li>
<li>Determine the position of objects with a series of reed sensors on a surface and put a magnet on your objects</li>
<li>Put magnets on people and create an interactive project that reacts to their proximity/touching to your weird motorized, light sculpture</li>
</ul>
<p><strong>Pros &amp; Cons</strong></p>
<ul>
<li>Pros
<ul>
<li>They are relatively cheap to buy online if you buy them in bulk (see links below to purchase)</li>
<li>Great for controlling/sensing things that get close but don’t touch</li>
<li>Great switch for things not attached to each other</li>
</ul>
</li>
<li>Cons
<ul>
<li>Reed sensors without casings or housings may be fragile and difficult to mount. They are made of glass.</li>
<li>You may need to add <a href="https://www.arduino.cc/en/Tutorial/Debounce">debouncing</a> in your code</li>
<li>If you buy the ones that already come with plastic casing, it may not have the right form factor for your project</li>
</ul>
</li>
</ul>
<p><strong>Example Data Sheet</strong><br />
With all sensors you will need to make sure they meet your needs for voltage and current as well as any dimensional requirements for your project. Specific key specs to look at when shopping for these switches are:</p>
<ul>
<li>Is it normally open or normally closed?</li>
<li>At what distance does the switch change its state?</li>
</ul>
<p>Here is an example of important specs from <a href="https://www.adafruit.com/product/375">Adafruit’s magnetic contact switch</a>.</p>
<ul>
<li>Normally open reed switch</li>
<li>ABS enclosure</li>
<li>Rated current: 100 mA max</li>
<li>Rated voltage: 200 VDC max</li>
<li>Distance: 15mm max</li>
</ul>
<p>Dimensions:</p>
<ul>
<li>Box size (each side): 29mm x 14mm x 9mm / 1.1" x 0.6" x 0.4"</li>
<li>Cable Length: 305mm ± 12mm / 12" ± 0.5"</li>
<li>Weight (per side): 5.4g</li>
</ul>
<p><strong>How to use with an Arduino Uno (Example from SparkFun)</strong><br />
<em>Wiring your switch</em><br />
Put one end to ground, and put the other one into a digital pin.</p>
<img class="wp-image-623" src="{{ site.baseurl }}/assets/old-wp-content/example-arduino-circuit.png" alt="" />
###### Example circuit schematic from SparkFun
<br>
<p><em>Writing the Arduino code</em><br />
<script src="https://gist.github.com/bevchou/a8fa7155562239ea3125cf8cdff5e58a.js"></script></p>
<p><strong>Where to buy (as of February 2018)</strong><br />
<em>Magnetic Contact Switch</em><br />
<a href="http://a.co/4dWyKak">http://a.co/4dWyKak </a>- NC, circular enlosure, $7.59/pack of 5<br />
<a href="http://a.co/gXbgtB9">http://a.co/gXbgtB9</a> - NO, screw mount, $14.47/pack of 10<br />
<a href="https://www.adafruit.com/product/375">https://www.adafruit.com/product/375</a> - NO, screw mount, $3.95/each</p>
<p><em>Just the reed switch</em><br />
<a href="https://www.sparkfun.com/products/8642">https://www.sparkfun.com/products/8642</a> - NO, $1.95/each<br />
<a href="http://a.co/6J0gZMf">http://a.co/6J0gZMf</a> - NO, $8.88/pack of 10</p>
<p><strong>Citations &amp; References</strong><br />
<a href="http://www.explainthatstuff.com/howreedswitcheswork.html">Woodford, Chris. (2009/2017) Reed switches.</a><br />
<a href="https://learn.sparkfun.com/tutorials/reed-switch-hookup-guide?_ga=2.183606246.1353928280.1519160810-1278440975.1519160810">SparkFun’s Guide to Reed Switches</a><br />
<a href="https://standexelectronics.com/resources/technical-library/technical-papers/reed-sensor-applications/">Reed Sensor Applications from Standex Electronic</a></p>
