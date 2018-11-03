---
layout: post
title: Final Haptics Project - Petting A Cat
date: 2018-11-3
type: post
categories:
- Haptics
tags:
- Sensors
- Motors
- Haptics
- Cats
meta:
author:
   Beverly
---

![gif of haptic motor]({{ site.baseurl }}/assets/haptics/final-petting-cat.gif)

For our final project, we decided to make an improved version of our previous project where you pet a cat which causes it to purr. To make the experience more realistic we made the cat to purr only when petting in one direction and improve the purring vibration feeling from the haptic motors.

<!--more-->

In addition to changing the design, we also used wire wrapping to create better connections and reduce the use of alligator clips. We placed the two square FSRs next to each other so we could better sense which direction the user is moving their hand. We also experimented with the motor placement. We started with the motors embedded into the cardboard.

![motors in cardboard]({{ site.baseurl }}/assets/haptics/final-motors-embedded.jpg)

But this did not provide as strong of a vibration because I think some of the vibration was subdued by the cardboard. We went back to our previous design of having the motors sit on top of the cardboard. The fur was able to hide the lumpiness of the motors, but we probably needed to experiment with more mounting methods to get the most accurate feeling of a cat purr.

![final design under the fur]({{ site.baseurl }}/assets/haptics/final-last-pcomp-design.jpg)

We also updated the code so that the cat would purr 3 times (instead of only once) after one pet. Only one purr seemed to abrupt and I think it gave better feedback to encourage the user to keep petting the cat. Finally, we added a tail so users would know which way to pet the cat. We installed it for the day in the ITP lounge. Hopefully it was a nice experience for any stressed out ITPers on the floor that day.

![final install in lounge]({{ site.baseurl }}/assets/haptics/final-lounge-install.jpg)


### The Arduino Code

This is our code that runs on the Arduino Uno. Caleb wrote pretty much all of the code.

{% highlight cpp %}
//vibrating motor pins
#define PINA 11
#define PINB 10
#define PINC 9

//force sensor pins
int FSRA = A0;
int FSRB = A1;


int buzzThreshold = 255;      //max strength of cat purr
int petThreshold = 40;
int fsrAreading;          // the analog reading from the FSR resistor divider
int fsrBreading;          // t  he analog reading from the FSR resistor divider
bool pettingNow = false;

void setup() {
  Serial.begin(9600);   // We'll send debugging information via the Serial monitor

}

void loop() {
  fsrAreading = analogRead(FSRA);
  fsrBreading = analogRead(FSRB);
  Serial.print("A reading: ");
  Serial.print(fsrAreading);
  Serial.print("  | B reading: ");
  Serial.println(fsrBreading);


  //Easy option: nested if
  if (fsrAreading >= petThreshold) {
    Serial.println("first sensor stroked");
    if (fsrBreading >= petThreshold) {
      Serial.println("second sensor stroked too");
      pettingNow = true;
      if (pettingNow == true) {
        purr(); purr(); purr();
        pettingNow = false;
      }
    }
  }
}

void purr() {
  for (int fadeValue = 0 ; fadeValue <= buzzThreshold; fadeValue += 4) {
    // sets the value (range from 0 to 255):
    analogWrite(PINA, fadeValue);
    analogWrite(PINB, fadeValue);
    analogWrite(PINC, fadeValue);
    // wait for 30 milliseconds to see the dimming effect
    delay(20);
  }

  // fade out from max to min in increments of 5 points:
  for (int fadeValue = buzzThreshold ; fadeValue >= 0; fadeValue -= 4) {
    // sets the value (range from 0 to 255):
    analogWrite(PINA, fadeValue);
    analogWrite(PINB, fadeValue);
    analogWrite(PINC, fadeValue);
    // wait for 30 milliseconds to see the dimming effect
    delay(20);
  }
}
{% endhighlight %}
