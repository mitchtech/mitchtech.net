---
author: michael
comments: true
date: 2012-05-02 04:35:48+00:00
layout: post
link: http://mitchtech.net/android-arduino-usb-host-combination-lock/
slug: android-arduino-usb-host-combination-lock
title: Android + Arduino + USB Host + Combination Lock
categories:
- ADB Microbridge
- Android
- Arduino
- Tutorials
tags:
- ADB
- Analog Output
- Android
- Arduino
- Electronics
- Lock
- Microbridge
- Microcontroller
- USB Host
---

{{< youtube XI2ApLNNc7A >}}

A simple combination lock with Android and Arduino.  The fancy wheel scroller is based on the [android-wheel ](http://code.google.com/p/android-wheel/)widget from [yuri kanivets.](http://android-devblog.blogspot.com/)

For additional background information on interfacing Android with the real world, check out my other introductory tutorials:

[Simple Digital Input](http://mitchtech.net/android-arduino-usb-host-simple-digital-input/)
[Simple Digital Output](http://mitchtech.net/android-arduino-usb-host-simple-digital-output/)
[Simple Analog Input](http://mitchtech.net/android-arduino-usb-host-simple-analog-input/)
[Simple Analog Output](http://mitchtech.net/android-arduino-usb-host-simple-analog-output/)

## Hardware

#### Parts needed:

  * Android Device (1.6+)

  * Hobby servo

  * Breadboard

  * Power supply

  * Hook-up wire

  * Android ADK Board*

  * – OR –

  * Arduino compatible and USB Host shield

*Supported boards include:

[Google ADK board](http://www.rt-net.jp/shop/index.php?main_page=product_info&cPath=3_4&products_id=1), [Freeduino ADK board ](http://shop.moderndevice.com/products/freeduino-usb-host-board), [Seeed Studio ADK board](http://www.seeedstudio.com/depot/seeeduino-adk-main-board-p-846.html), and [DIY Drones ADK board](https://store.diydrones.com/ProductDetails.asp?ProductCode=BR-PhoneDrone)

#### Assembly

Simply connect the black line to ground, the red line to +5v, and the yellow signal line to Arduino pin 5 (or other PWM capable pin, usually marked with a ~ symbol). Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/adb_combination_lock.png)](http://mitchtech.net/wp-content/uploads/2012/05/adb_combination_lock.png)

## Software

#### Arduino Firmware

Next, upload the Arduino sketch to the microcontroller. The sketch uses the [Microbridge](http://code.google.com/p/microbridge/) implementation by Niels Brouwers. Microbridge uses Android Debug Bridge (ABD) forwarding over TCP, rather than the official Google Android ADK. You can checkout the source for the Arduino sketch from Github, or just copy and paste the following into the Arduino IDE.

{{< gist mitchtech 1695856 >}}

#### Android App

Finally, install the Android Demo application onto the device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/adb/AdbCombinationLock.apk)or checkout the source from [Github](https://github.com/mitchtech/android_adb_combination_lock):

```
git clone git://github.com/mitchtech/android_adb_combination_lock.git
```

Finally upload the app to the device (or browse to this page on the device and download the apk above). Connect the Android device to the USB Host board/shield, and start up the app.

