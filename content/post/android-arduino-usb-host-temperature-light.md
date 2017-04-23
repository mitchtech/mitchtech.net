---
author: michael
comments: true
date: 2012-05-02 04:41:37+00:00
layout: post
link: http://mitchtech.net/android-arduino-usb-host-temperature-light/
slug: android-arduino-usb-host-temperature-light
title: Android + Arduino + USB Host + Temperature + Light
categories:
- ADB Microbridge
- Android
- Arduino
- Tutorials
tags:
- ADB
- Ambient Light
- Analog Input
- Android
- Arduino
- Electronics
- Graph
- Microbridge
- Microcontroller
- Photocell
- Sensor
- Temperature
- USB Host
- Voltage Divider
---

{{< youtube 0Eu3c4dQP8c >}}

Sensing temperature and light with Android and Arduino.  This article will demonstrate a basic thermometer / ambient light level detection input accessory.

For additional background information on interfacing Android with the real world, check out my other introductory tutorials:

[Simple Digital Input](http://mitchtech.net/android-arduino-usb-host-simple-digital-input/)
[Simple Digital Output](http://mitchtech.net/android-arduino-usb-host-simple-digital-output/)
[Simple Analog Input](http://mitchtech.net/android-arduino-usb-host-simple-analog-input/)
[Simple Analog Output](http://mitchtech.net/android-arduino-usb-host-simple-analog-output/)

## Hardware

#### Parts needed:

  * Android Device (1.6+)

  * Photocell

  * 10K ohm resistor

  * TMP36 temperature sensor

  * Hook-up wire

  * Android ADK Board*

  * – OR –

  * Arduino compatible and USB Host shield

*Supported boards include:

[Google ADK board](http://www.rt-net.jp/shop/index.php?main_page=product_info&cPath=3_4&products_id=1), [Freeduino ADK board ](http://shop.moderndevice.com/products/freeduino-usb-host-board), [Seeed Studio ADK board](http://www.seeedstudio.com/depot/seeeduino-adk-main-board-p-846.html), and [DIY Drones ADK board](https://store.diydrones.com/ProductDetails.asp?ProductCode=BR-PhoneDrone)

#### Assembly

Connect one of the photocell leads to 5v and the other to analog input pin A0. Also connect the same lead through a 10K resistor to ground.  In hardware, this concept is known as a [voltage divider](http://en.wikipedia.org/wiki/Voltage_divider).  Then connect the ground and power leads of the TMP36 to, you guessed it, ground and 5V.  Finally, connect the signal lead of the TMP36 to analog input pin A1. Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/adb_temp_light.png)](http://mitchtech.net/wp-content/uploads/2012/05/adb_temp_light.png)

## Software

#### Arduino Firmware

Next, upload the Arduino sketch to the microcontroller. The sketch uses the [Microbridge](http://code.google.com/p/microbridge/) implementation by Niels Brouwers. Microbridge uses Android Debug Bridge (ABD) forwarding over TCP, rather than the [Google Android ADK](http://developer.android.com/guide/topics/usb/adk.html). You can checkout the source for the Arduino sketch from Github, or just copy and paste the following into the Arduino IDE.

{{< gist mitchtech 1701112 >}}

#### Android App

The next step is to install the Android Demo application onto the device. You can either [download the pre-built .apk ](http://mitch-tech.appspot.com/adb/AdbTempLight.apk)or checkout the source from [Github](https://github.com/mitchtech/android_adb_temp_light):

```
git clone git://github.com/mitchtech/android_adb_temp_light.git
```

Finally upload the app to the device (or browse to this page on the device and download the apk above).  Connect the Android device to the USB Host board/shield, and start up the app.

