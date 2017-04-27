+++
author = "michael"
categories = ["Android","IOIO","Tutorials"]
comments = true
date = "2012-05-02 04:00:53+00:00"
slug = "android-ioio-seven-segment-led"
tags = ["Android","Bluetooth","Digital Output","Electronics","IOIO","LED","Microcontroller","PIC","Seven Segment"]
title = "Android + IOIO + Seven Segment LED"

+++

{{< youtube QoHnJwbX_fQ >}}

Basic control of a seven segment LED display with IOIO and Android.

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

  * Seven segment LED display

  * 330k ohm resistors

  * Breadboard

  * Power supply

  * Hook-up wire

#### Assembly

The LED display is common anode with pins 3 and 8 (top center and bottom center) to ground with a current limiting 330 ohm resistor in series.  Connect the seven segment pins as shown below to IOIO pins 34 -40. The code can be modified for use with any other IO pins (all IOIO pins are GPIO pins). Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/ioio_seven_segment_led.png)](http://mitchtech.net/wp-content/uploads/2012/05/ioio_seven_segment_led.png)

## Software

#### Get the source

With the circuit assembled, the next step is to get the demo application on the Android device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/ioio/IOIOSevenSegmentLed.apk) or checkout the source from [Github](https://github.com/mitchtech/android_ioio_seven_segment_led):

```
git clone git://github.com/mitchtech/android_ioio_seven_segment_led.git
```

If you are building from source, you will also need to import the IOIO Library project, and optionally the IOIO Bluetooth library projects, both available [here](https://github.com/ytai/ioio):

```
git clone git://github.com/ytai/ioio.git
```

#### Install, connect, profit!

Finally, upload the app to the Android device (or browse to this page on the device and download the apk above). Connect the device to the IOIO, and start up the app.

