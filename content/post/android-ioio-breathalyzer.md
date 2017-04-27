+++
author = "michael"
categories = ["Android","IOIO","Tutorials"]
comments = true
date = "2012-05-02 04:12:12+00:00"
slug = "android-ioio-breathalyzer"
tags = ["Analog Input","Android","Bluetooth","Breathalyzer","Electronics","Graph","IOIO","Microcontroller","PIC","Sensor"]
title = "Android + IOIO + Breathalyzer"

+++

{{< youtube RTHdzqqf5ak >}}

Proof of concept breathalyzer powered by Android and IOIO.  This article will demonstrate a basic alcohol gas detection device for Android over USB (or bluetooth).

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

  * 330 ohm resistor

  * Alcohol Gas Sensor MQ-3 (available at [Sparkfun](http://www.sparkfun.com/products/8880))

  * Breadboard

  * Power supply

  * Hook-up wire

#### Assembly

Connect the red, power lines of the MQ-3 to +5v, the black ground line to GND, and the analog signal lines to the desired input pin. The example uses pins 34 but can be used with other pins that support analog input (pins 31 – 46 on the IOIO). Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/ioio_breathalyzer.png)](http://mitchtech.net/wp-content/uploads/2012/05/ioio_breathalyzer.png)

## Software

#### Get the source

With the circuit assembled, the next step is to get the demo application on the Android device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/ioio/IOIOBreathalyzer.apk) or checkout the source from [Github](https://github.com/mitchtech/android_ioio_breathalyzer):

```
git clone git://github.com/mitchtech/android_ioio_breathalyzer.git
```

If you are building from source, you will also need to import the IOIO Library project, and optionally the IOIO Bluetooth library projects, both available [here](https://github.com/ytai/ioio):

```
git clone git://github.com/ytai/ioio.git
```

#### Install, connect, profit!

Finally, upload the app to the Android device (or browse to this page on the device and download the apk above). Connect the device to the IOIO, and start up the app.

