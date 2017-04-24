+++
author = "michael"
categories = ["Android","IOIO","Tutorials"]
comments = true
date = "2012-05-02 04:26:28+00:00"
slug = "android-ioio-countdown-timer"
tags = ["Android","Bluetooth","Digital Output","Electronics","IOIO","LED","Microcontroller","PIC","Timer"]
title = "Android + IOIO + Countdown Timer"

+++

{{< youtube jx2uM9pz87o >}}

Countdown timer Android app with IOIO output. When the timer goes off, it pulls the pin high, or low.  The article demonstrates a proof of concept usage with a single LED, but this could easily be adapted for other usages: light switches and appliance control, detonators, etc.

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

  * LED

  * 330 ohm resistor

  * Breadboard

  * Power supply

  * Hook-up wire

#### Assembly

For instructions and diagram, check out:  [Android + IOIO + Simple Digital Output](http://mitchtech.net/android-ioio-simple-digital-output/)

## Software

#### Get the source

With the circuit assembled, the next step is to get the demo application on the Android device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/ioio/IOIOCountdownTimer.apk) or checkout the source from [Github](https://github.com/mitchtech/android_ioio_countdown_timer):

```
git clone git://github.com/mitchtech/android_ioio_countdown_timer.git
```

If you are building from source, you will also need to import the IOIO Library project, and optionally the IOIO Bluetooth library projects, both available [here](https://github.com/ytai/ioio):

```
git clone git://github.com/ytai/ioio.git
```

#### Install, connect, profit!

Finally, upload the app to the Android device (or browse to this page on the device and download the apk above). Connect the device to the IOIO, and start up the app.

#### Controlling other devices

Here’s an updated video using the same source code and essentially the same circuit (transistor controlled relay) to control a 12V fire alarm bell.

{{< youtube CVHCrTTqjUE >}}
