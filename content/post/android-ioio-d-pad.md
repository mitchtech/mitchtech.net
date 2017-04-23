---
author: michael
comments: true
date: 2012-05-02 03:50:57+00:00
layout: post
link: http://mitchtech.net/android-ioio-d-pad/
slug: android-ioio-d-pad
title: Android + IOIO + D-Pad
categories:
- Android
- IOIO
- Tutorials
tags:
- Android
- Bluetooth
- Buttons
- D Pad
- Digital Input
- Electronics
- IOIO
- Microcontroller
- PIC
---

{{< youtube lrGkvYAd12c >}}

A simple controller for use as an Android D-pad (directional pad) input accessory.  The IOIO based device uses four momentary push buttons to sense digital inputs for up, down, left, and right.

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

  * 4x Push button

  * Breadboard

  * Power supply

  * Hook-up wire

#### Assembly

Connect one side of each button to ground and the other side to the desired digital input pins on the IOIO. The example uses pins 34-37, but can be used with any IO pins (all IOIO pins are GPIO pins). Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/ioio_d_pad.png)](http://mitchtech.net/wp-content/uploads/2012/05/ioio_d_pad.png)

## Software

#### Get the source

With the circuit assembled, the next step is to get the demo application on the Android device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/ioio/IOIODPad.apk) or checkout the source from [Github](https://github.com/mitchtech/android_ioio_d_dap):

```
git clone git://github.com/mitchtech/android_ioio_d_pad.git
```

If you are building from source, you will also need to import the IOIO Library project, and optionally the IOIO Bluetooth library projects, both available [here](https://github.com/ytai/ioio):

```
git clone git://github.com/ytai/ioio.git
```

#### Install, connect, profit!

Finally, upload the app to the Android device (or browse to this page on the device and download the apk above). Connect the device to the IOIO, and start up the app.

