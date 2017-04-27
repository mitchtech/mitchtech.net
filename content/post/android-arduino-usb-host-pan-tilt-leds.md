+++
author = "michael"
categories = ["ADB Microbridge","Android","Arduino","Tutorials"]
comments = true
date = "2012-05-02 04:40:30+00:00"
slug = "android-arduino-usb-host-pan-tilt-leds"
tags = ["ADB","Analog Output","Android","Arduino","Digital Output","Electronics","LED","Microbridge","Microcontroller","Pan &amp; Tilt","PWM","Servo","USB Host"]
title = "Android + Arduino + USB Host + Pan Tilt LEDs"

+++

{{< youtube oDpVTzXstBc >}}

Combining analog and digital outputs with Android and Arduino.  This tutorial will demonstrate the basics for using two servos to achieve basic basic pan and tilt functionality. In addition, digital control is demonstrated using two LEDs.

For additional background information on interfacing Android with the real world, check out my other introductory tutorials:

[Simple Digital Input](http://mitchtech.net/android-arduino-usb-host-simple-digital-input/)

[Simple Digital Output](http://mitchtech.net/android-arduino-usb-host-simple-digital-output/)

[Simple Analog Input](http://mitchtech.net/android-arduino-usb-host-simple-analog-input/)

[Simple Analog Output](http://mitchtech.net/android-arduino-usb-host-simple-analog-output/)

## Hardware

#### Parts needed:

  * Android Device (1.6+)

  * 2x Hobby servos

  * Pan / tilt bracket assembly

  * 2x LEDs

  * 2x 330 ohm resistors

  * Breadboard

  * Power supply

  * Hook-up wire

  * Android ADK Board*

  * – OR –

  * Arduino compatible and USB Host shield

*Supported boards include:

[Google ADK board](http://www.rt-net.jp/shop/index.php?main_page=product_info&cPath=3_4&products_id=1), [Freeduino ADK board ](http://shop.moderndevice.com/products/freeduino-usb-host-board), [Seeed Studio ADK board](http://www.seeedstudio.com/depot/seeeduino-adk-main-board-p-846.html), and [DIY Drones ADK board](https://store.diydrones.com/ProductDetails.asp?ProductCode=BR-PhoneDrone)

#### Assembly

Connect the red, power lines of the servos to +5v, the black ground lines to GND, and the yellow signal lines to the desired output pins, 5 and 6 in the example (others can be used, but must be PWM capable).  Also, connect the 330 ohm resistors in series with the anodes of the LEDs to the desired digital output pins, and the cathodes of the LEDs to ground.  Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/adb_pan_tilt_leds.png)](http://mitchtech.net/wp-content/uploads/2012/05/adb_pan_tilt_leds.png)

## Software

#### Arduino Firmware

Next, upload the Arduino sketch to the microcontroller. The sketch uses the [Microbridge](http://code.google.com/p/microbridge/) implementation by Niels Brouwers. Microbridge uses Android Debug Bridge (ABD) forwarding over TCP, rather than the official Google Android ADK. You can checkout the source for the Arduino sketch from Github, or just copy and paste the following into the Arduino IDE.

{{< gist mitchtech 1695867 >}}

#### Android App

Finally, install the Android Demo application onto the device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/adb/AdbPanTiltLeds.apk)or checkout the source from [Github](https://github.com/mitchtech/android_adb_pan_tilt_leds):

```
git clone git://github.com/mitchtech/android_adb_pan_tilt_leds.git
```

Finally upload the app to the device (or browse to this page on the device and download the apk above). Connect the Android device to the USB Host board/shield, and start up the app.

