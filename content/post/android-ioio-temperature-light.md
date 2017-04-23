---
author: michael
comments: true
date: 2012-05-02 04:28:06+00:00
layout: post
link: http://mitchtech.net/android-ioio-temperature-light/
slug: android-ioio-temperature-light
title: Android + IOIO + Temperature + Light
categories:
- Android
- IOIO
- Tutorials
tags:
- Ambient Light
- Analog Input
- Android
- Bluetooth
- Digital Input
- Electronics
- Graph
- IOIO
- Microcontroller
- Photocell
- PIC
- Sensor
- Temperature
- Voltage Divider
---

{{< youtube BdLr5a__ySc >}}

Sensing temperature and light with Android and IOIO.  This article will demonstrate a basic thermometer / ambient light level detection input accessory.

For additional background information on interfacing Android with IOIO, check out my other introductory tutorials:

[Android + IOIO + Simple Digital Output](http://mitchtech.net/android-ioio-simple-digital-output/)
[Android + IOIO + Simple Digital Input](http://mitchtech.net/android-ioio-simple-digital-input/)
[Android + IOIO + Simple Analog Output](http://mitchtech.net/android-ioio-simple-analog-output/)
[Android + IOIO + Simple Analog Input](http://mitchtech.net/android-ioio-simple-analog-input/)

Background on Android development, IOIO, and electronics:

[Meet IOIO](http://ytai-mer.blogspot.com/2011/04/meet-ioio-io-for-android.html)
[IOIO for Android Beginners Guide](http://www.sparkfun.com/tutorials/280)
[IOIO Wiki](https://github.com/ytai/ioio/wiki)
[Android Developer’s Guide](http://developer.android.com/guide/index.html)

## Hardware

#### Parts needed:

  * Android Device (1.6+, 2.1 for Bluetooth)

  * IOIO (available at [Sparkfun](http://www.sparkfun.com/products/10748))

  * Photocell

  * 10k ohm resistors

  * TMP36 temperature sensor

  * Breadboard

  * Power supply

  * Hook-up wire

#### Assembly

Connect the ground and power leads of the TMP36 to GND and +3.3V respectively, and connect the center signal lead of the TMP36 to the desired input pin (34 below).  Then connect one lead of the photocell to +3.3V and the other to the desired analog input pin (pin 35 below). Also connect the same lead through a 10K resistor to ground creating a [voltage divider](http://en.wikipedia.org/wiki/Voltage_divider).   Other IOIO pins can be used, as long as they support analog input (pins 31 – 46 on the IOIO). Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/ioio_temp_light.png)](http://mitchtech.net/wp-content/uploads/2012/05/ioio_temp_light.png)

## Software

#### Get the source

With the circuit assembled, the next step is to get the demo application on the Android device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/ioio/IOIOTempLight.apk) or checkout the source from [Github](https://github.com/mitchtech/android_ioio_temp_light):

```
git clone git://github.com/mitchtech/android_ioio_temp_light.git
```

If you are building from source, you will also need to import the IOIO Library project, and optionally the IOIO Bluetooth library projects, both available [here](https://github.com/ytai/ioio):

```
git clone git://github.com/ytai/ioio.git
```

#### Install, connect, profit!

Finally, upload the app to the Android device (or browse to this page on the device and download the apk above). Connect the device to the IOIO, and start up the app.

