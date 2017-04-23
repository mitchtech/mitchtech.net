---
author: michael
comments: true
date: 2012-05-02 04:45:59+00:00
layout: post
link: http://mitchtech.net/android-ioio-laser-turret/
slug: android-ioio-laser-turret
title: Android + IOIO + Laser Turret
categories:
- Android
- IOIO
- Tutorials
tags:
- Analog Output
- Android
- Bluetooth
- Digital Output
- Electronics
- IOIO
- Laser
- LED
- Microcontroller
- Pan &amp; Tilt
- PIC
- Servo
---

{{< youtube y8anHCh1Tjo >}}

Android and IOIO powered pan and tilt bracket with dual lasers. Pew pew!

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

  * 2x Hobby servo

  * 2x 10k ohm resistors

  * 2x Laser (like this one at [DealExtreme](http://dx.com/p/6mm-5mw-red-laser-module-3-5-4-5v-13378?Utm_rid=33954493&Utm_source=affiliate))

  * Breadboard

  * Power supply

  * Hook-up wire

#### Assembly

Connect the red, power lines of the servos to +5v, the black ground lines to GND, and the yellow signal lines to the desired output pins, number 3 and 6 in the example below.  Other pins can be used as long as they support peripheral output (for PWM, marked with the letter ‘p’ on the back of the IOIO) AND are 5V tolerant (marked with a black circle around the pin). This leaves pins 3-7, and 10-14 as the only potentials.  Also, connect the same signal lines to +5V, with a 10k ohm resistor in series.  This allows use of the pins in 5V open drain mode, required since the IOIO operates with 3.3V. Also connect the red leads of the lasers to +3.3V and the black leads to pins 34 and 35 (any GPIO pins can be used). Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/ioio_laser_turret.png)](http://mitchtech.net/wp-content/uploads/2012/05/ioio_laser_turret.png)

## Software

#### Get the source

With the circuit assembled, the next step is to get the demo application on the Android device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/ioio/IOIOLaserTurret.apk) or checkout the source from [Github](https://github.com/mitchtech/android_ioio_laser_turret):

```
git clone git://github.com/mitchtech/android_ioio_laser_turret.git
```

If you are building from source, you will also need to import the IOIO Library project, and optionally the IOIO Bluetooth library projects, both available [here](https://github.com/ytai/ioio):

```
git clone git://github.com/ytai/ioio.git
```

#### Install, connect, profit!

Finally, upload the app to the Android device (or browse to this page on the device and download the apk above). Connect the device to the IOIO, and start up the app.

