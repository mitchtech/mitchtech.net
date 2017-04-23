---
author: michael
comments: true
date: 2012-05-02 04:39:18+00:00
layout: post
link: http://mitchtech.net/android-arduino-usb-host-serial-4-digit-led/
slug: android-arduino-usb-host-serial-4-digit-led
title: Android + Arduino + USB Host + Serial 4 digit LED
categories:
- ADB Microbridge
- Android
- Arduino
- Tutorials
tags:
- ADB
- Android
- Arduino
- Digital Output
- Electronics
- LED
- Microbridge
- Microcontroller
- Seven Segment
- USB Host
---

{{< youtube 1wpE_HzTfl0 >}}

Interfacing a serial display with Android and Arduino.  This article will demonstrate communication of a serial 7 segment display, specifically this one: [7-Segment Serial Display – Blue](http://www.sparkfun.com/products/9765) from [Sparkfun](http://www.sparkfun.com/) electronics.  The fancy wheel scroller is based on the [android-wheel ](http://code.google.com/p/android-wheel/)widget from [yuri kanivets.](http://android-devblog.blogspot.com/)

For additional background information on interfacing Android with the real world, check out my other introductory tutorials:

[Simple Digital Input](http://mitchtech.net/android-arduino-usb-host-simple-digital-input/)
[Simple Digital Output](http://mitchtech.net/android-arduino-usb-host-simple-digital-output/)
[Simple Analog Input](http://mitchtech.net/android-arduino-usb-host-simple-analog-input/)
[Simple Analog Output](http://mitchtech.net/android-arduino-usb-host-simple-analog-output/)

## Hardware

#### Parts needed:

  * Android Device (1.6+)

  * 7-Segment Serial Display

  * Hook-up wire

  * Android ADK Board*

  * – OR –

  * Arduino compatible and USB Host shield

*Supported boards include:

[Google ADK board](http://www.rt-net.jp/shop/index.php?main_page=product_info&cPath=3_4&products_id=1), [Freeduino ADK board ](http://shop.moderndevice.com/products/freeduino-usb-host-board), [Seeed Studio ADK board](http://www.seeedstudio.com/depot/seeeduino-adk-main-board-p-846.html), and [DIY Drones ADK board](https://store.diydrones.com/ProductDetails.asp?ProductCode=BR-PhoneDrone)

#### Assembly

This display can be controlled with either SPI or serial TTL communication.  However, since the SPI pins are required for communication with the USB Host, TTL serial must be used (this also requires fewer pins, one instead of three).   So, connect the RX pin on the serial display to the serial TX pin on the Arduino (determined by the firmware sketch) and connect GND and VCC on the serial display to ground and+5v respectively.  Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/adb_serial_4_digit_led.png)](http://mitchtech.net/wp-content/uploads/2012/05/adb_serial_4_digit_led.png)

## Software

#### Arduino Firmware

Next, upload the Arduino sketch to the microcontroller. The sketch uses the [Microbridge](http://code.google.com/p/microbridge/) implementation by Niels Brouwers. Microbridge uses Android Debug Bridge (ABD) forwarding over TCP, rather than the [Google Android ADK](http://developer.android.com/guide/topics/usb/adk.html). You can checkout the source for the Arduino sketch from Github, or just copy and paste the following into the Arduino IDE.

{{< gist mitchtech 1701106 >}}

#### Android App

The next step is to install the Android Demo application onto the device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/adb/AdbSerial4DigitLed.apk) or checkout the source from [Github](https://github.com/mitchtech/android_adb_serial_4_digit_led):

```
git clone git://github.com/mitchtech/android_adb_serial_4_digit_led.git
```

Finally upload the app to the device (or browse to this page on the the device and download the apk above).  Connect the Android device to the USB Host board/shield, and start up the app.
