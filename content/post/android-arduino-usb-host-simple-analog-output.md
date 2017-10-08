+++
author = "michael"
categories = ["ADB Microbridge","Android","Arduino","Tutorials"]
comments = true
date = "2012-05-02 03:09:33+00:00"
slug = "android-arduino-usb-host-simple-analog-output"
tags = ["ADB","Analog Output","Android","Arduino","Electronics","LED","Microbridge","Microcontroller","PWM","RGB LED","USB Host"]
title = "Android + Arduino + USB Host + Simple Analog Output"

+++

{{< youtube vRzKFiYzxUQ >}}

Simplest possible analog output with Android and Arduino. This article will discuss the bare minimal requirements for development of an Android USB digital output device, a controllable RGB LED. The goal is to demonstrate the easiest possible use of the technology. For additional background information on Android development, Arduino, and MicroBridge, check out these links:

[Android Developer’s Guide](http://developer.android.com/guide/index.html)

[Getting Started with Arduino](http://arduino.cc/en/Guide/HomePage)

[Microbridge](http://code.google.com/p/microbridge/)

## Getting Started

First, make sure you have setup the development environments for Arduino and Android:

[Arduino IDE](http://arduino.cc/en/Main/Software)

[Android SDK](http://developer.android.com/sdk/index.html)

## Hardware

#### Parts needed:

  * Android Device (1.6+)

  * RGB LED

  * 3x 330 ohms resistors

  * Breadboard

  * Power supply

  * Hook-up wire

  * Android ADK Board*

  * – OR –

  * Arduino compatible and USB Host shield

*Supported boards include:

[Google ADK board](http://www.rt-net.jp/shop/index.php?main_page=product_info&cPath=3_4&products_id=1), [Freeduino ADK board ](http://shop.moderndevice.com/products/freeduino-usb-host-board), [Seeed Studio ADK board](http://www.seeedstudio.com/depot/seeeduino-adk-main-board-p-846.html), and [DIY Drones ADK board](https://store.diydrones.com/ProductDetails.asp?ProductCode=BR-PhoneDrone)

#### Assembly

The RGB LED has four leads: the three short ones are anodes that correspond to each of the three colors (red, green, and blue) and the fourth, longer lead is the common cathode.  Connect the 330 ohm resistors in series with the anodes of the LED and the common cathode to ground. The example uses pins 3, 5, and 6, but can be used with any PWM pin (usually denoted with a ~ symbol) that doesn’t interfere with the SPI communication with the USB Host Board (usually pins 10 – 14).  The resistors, in this case, are being used to prevent current overdraw to the LEDs. Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

![adb_simple_analog_output](/img/adb_simple_analog_output.png)

## Software

#### Arduino Firmware

Next, upload the Arduino sketch to the microcontroller. The sketch uses the [Microbridge](http://code.google.com/p/microbridge/)implementation by Niels Brouwers. Microbridge uses Android Debug Bridge (ABD) forwarding over TCP, rather than the official Google Android ADK. You can checkout the source for the Arduino sketch from Github, or just copy and paste the following into the Arduino IDE.

{{< gist mitchtech 1686179 >}}

#### Android App

Finally, install the Android Demo application onto the device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/adb/AdbSimpleAnalogOutput.apk)or checkout the source from [Github](https://github.com/mitchtech/android_adb_simple_analog_output):

```
git clone git://github.com/mitchtech/android_adb_simple_analog_output.git
```

Finally upload the app to the device (or browse to this page on the device and download the apk above). Connect the Android device to the USB Host board/shield, and start up the app.
