---
layout: post
title: "XBee Setup Tutorial"
categories:
  - Programming
  - Electronics
  - Robotics
image: assets/images/mechanical_engineering.jpg
description: "A guide to configuring XBee wireless radio modules using X-CTU and CLI"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2010/10/11/xbee-setup-tutorial/](https://blog.henrypoon.com/blog/2010/10/11/xbee-setup-tutorial/)

This article (link at the bottom) is very useful for beginners that want to use XBee's for wireless radio communication. It discusses the basics of using XBee's, such as using the computer to configure various options within the XBee such as the baud rate, network ID, etc. It discusses two methods of setting the options in the XBee. One method is through a program called X-CTU (GUI) and another method is using a CLI. The important options in the XBee are discussed and explained so that everyone knows what they should be set to.

The configuration that I used was that I had my computer connected to an XBee USB Explorer via USB. On the other end was an Arduino Duemilanove powered by six 1.2 V NiMH batteries, and this microcontroller powered the XBee using its 5 V pin. I compiled and downloaded the program at the bottom of the article to my Arduino and I tested it using the Serial Monitor that comes with the Arduino IDE.

Even though the test program is simple, it shows that a wireless link can be made between the computer and the microcontroller, meaning that the microcontroller can process computer input to do even more crazy things.

**Link**: <http://forums.trossenrobotics.com/tutorials/how-to-diy-128/xbee-basics-3259/>
