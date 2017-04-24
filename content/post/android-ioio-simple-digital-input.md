+++
author = "michael"
categories = ["Android","IOIO","Tutorials"]
comments = true
date = "2012-05-02 03:33:47+00:00"
layout = "post"
link = "http://mitchtech.net/android-ioio-simple-digital-input/"
slug = "android-ioio-simple-digital-input"
tags = ["Android","Bluetooth","Buttons","Digital Input","Electronics","IOIO","Microcontroller","PIC"]
title = "Android + IOIO + Simple Digital Input"

+++

{{< youtube Cr2PpNiEDXI >}}

Simplest possible digital input with Android and IOIO. This article will discuss the bare minimal requirements for development of an Android USB (or Bluetooth) digital input device.

The goal is to demonstrate the easiest possible use of the technology. For additional background information on Android development, IOIO, and electronics, check out these links:

[Meet IOIO](http://ytai-mer.blogspot.com/2011/04/meet-ioio-io-for-android.html)
[IOIO for Android Beginners Guide](http://www.sparkfun.com/tutorials/280)
[IOIO Wiki](https://github.com/ytai/ioio/wiki)
[Android Developer’s Guide](http://developer.android.com/guide/index.html)

## Hardware

#### Parts needed:

  * Android Device (1.6+, 2.1 for Bluetooth)

  * IOIO (available at [Sparkfun](http://www.sparkfun.com/products/10748))

  * 2x Push button

  * Breadboard

  * Power supply

  * Hook-up wire

#### Assembly

Connect one side of each button to ground and the other side to the digital input pins. The example uses pins 34 and 35 but can be used with any IO pin (all IOIO pins are GPIO pins). Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/ioio_simple_digital_input.png)](http://mitchtech.net/wp-content/uploads/2012/05/ioio_simple_digital_input.png)

## Software

#### Get the source

With the circuit assembled, the next step is to get the demo application on the Android device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/ioio/IOIOSimpleDigitalInput.apk) or checkout the source from [Github](https://github.com/mitchtech/android_ioio_simple_digital_input):

```
git clone git://github.com/mitchtech/android_ioio_simple_digital_input.git
```

If you are building from source, you will also need to import the IOIO Library project, and optionally the IOIO Bluetooth library projects, both available [here](https://github.com/ytai/ioio):

```
git clone git://github.com/ytai/ioio.git
```

#### Install, connect, profit!

Finally, upload the app to the Android device (or browse to this page on the device and download the apk above). Connect the device to the IOIO, and start up the app.

