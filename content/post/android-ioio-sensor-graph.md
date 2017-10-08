+++
author = "michael"
categories = ["Android","IOIO","Tutorials"]
comments = true
date = "2012-05-02 03:55:09+00:00"
slug = "android-ioio-sensor-graph"
tags = ["Analog Input","Android","Bluetooth","Electronics","Graph","IOIO","Microcontroller","PIC","Potentiometer","Sensor"]
title = "Android + IOIO + Sensor Graph"

+++

{{< youtube 8YTY3gQKqFQ >}}

A simple app to visualize analog sensor input with Android and IOIO.  The example uses a rotary potentiometer, but could easily be used with other sensor inputs such as [temperature or ambient light](http://mitchtech.net/android-ioio-temperature-light/).

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

  * Rotary potentiometer

  * Breadboard

  * Power supply

  * Hook-up wire

#### Assembly

Connect one side of the potentiometer to +3.3V, the opposite side to GND, and the center wiper to the desired analog input pin on the IOIO. The example uses pin 34, but can be used with any other pin that supports analog input (pins 31 – 46 on the IOIO). Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

![](/img/ioio_simple_analog_input.png)

## Software

#### Get the source

With the circuit assembled, the next step is to get the demo application on the Android device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/ioio/IOIOSensorGraph.apk) or checkout the source from [Github](https://github.com/mitchtech/android_ioio_sensor_graph):

```
git clone git://github.com/mitchtech/android_ioio_sensor_graph.git
```

If you are building from source, you will also need to import the IOIO Library project, and optionally the IOIO Bluetooth library projects, both available [here](https://github.com/ytai/ioio):

```
git clone git://github.com/ytai/ioio.git
```

#### Install, connect, profit!

Finally, upload the app to the Android device (or browse to this page on the device and download the apk above). Connect the device to the IOIO, and start up the app.

