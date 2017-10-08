+++
author = "michael"
categories = ["ADB Microbridge","Android","Arduino","Tutorials"]
comments = true
date = "2012-05-02 04:30:29+00:00"
slug = "android-arduino-usb-host-sensor-graph"
tags = ["ADB","Analog Input","Android","Arduino","Electronics","Graph","Microbridge","Microcontroller","Potentiometer","Sensor","USB Host"]
title = "Android + Arduino + USB Host + Sensor Graph"
banner = "https://img.youtube.com/vi/EQ4ZctuXgxE/0.jpg"

+++

{{< youtube EQ4ZctuXgxE >}}

A simple app to visualize analog sensor input with Android and Arduino.

For additional background information on interfacing Android with the real world, check out my other introductory tutorials:

[Simple Digital Input](http://mitchtech.net/android-arduino-usb-host-simple-digital-input/)

[Simple Digital Output](http://mitchtech.net/android-arduino-usb-host-simple-digital-output/)

[Simple Analog Input](http://mitchtech.net/android-arduino-usb-host-simple-analog-input/)

[Simple Analog Output](http://mitchtech.net/android-arduino-usb-host-simple-analog-output/)

## Hardware

#### Parts needed:

  * Android Device (1.6+)

  * Potentiometer

  * Breadboard

  * Power supply

  * Hook-up wire

  * Android ADK Board*

  * – OR –

  * Arduino compatible and USB Host shield

*Supported boards include:

[Google ADK board](http://www.rt-net.jp/shop/index.php?main_page=product_info&cPath=3_4&products_id=1), [Freeduino ADK board ](http://shop.moderndevice.com/products/freeduino-usb-host-board), [Seeed Studio ADK board](http://www.seeedstudio.com/depot/seeeduino-adk-main-board-p-846.html), and [DIY Drones ADK board](https://store.diydrones.com/ProductDetails.asp?ProductCode=BR-PhoneDrone)

#### Assembly

Connect the two sides of the potentiometer to 5v and ground, and the center wiper to analog input pin A0. Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

![adb_sensor_graph](/img/adb_sensor_graph.png)

## Software

#### Arduino Firmware

Next, upload the Arduino sketch to the microcontroller. The sketch uses the [Microbridge](http://code.google.com/p/microbridge/) implementation by Niels Brouwers. Microbridge uses Android Debug Bridge (ABD) forwarding over TCP, rather than the official Google Android ADK. You can checkout the source for the Arduino sketch from Github, or just copy and paste the following into the Arduino IDE.

{{< gist mitchtech 1668640 >}}

#### Android App

Finally, install the Android Demo application onto the device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/adb/AdbSensorGraph.apk)or checkout the source from [Github](https://github.com/mitchtech/android_adb_sensor_graph):

```
git clone git://github.com/mitchtech/android_adb_sensor_graph.git
```

Finally upload the app to the device (or browse to this page on the device and download the apk above). Connect the Android device to the USB Host board/shield, and start up the app.

