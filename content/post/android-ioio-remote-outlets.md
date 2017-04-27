+++
author = "michael"
categories = ["Android","IOIO","Tutorials"]
comments = true
date = "2012-05-02 04:51:31+00:00"
slug = "android-ioio-remote-outlets"
tags = ["Android","Bluetooth","Digital Output","DIY","Electronics","Hack","Home Automation","IOIO","Microcontroller","PIC","Power Outlet"]
title = "Android + IOIO + Remote Outlets"

+++

{{< youtube DfsHccXEcDk >}}

This tutorial will demonstrate remote control of 3 AC outlets with Android and IOIO.  The tutorial uses the [3 Channel Remote AC Outlets ](http://dx.com/p/3-channel-wireless-remote-controlled-ac-power-adapters-set-110v-us-plug-82399?Utm_rid=33954493&Utm_source=affiliate)from DealExtreme.  The cost, less than $25 shipped for the set of three, is quite a savings over alternatives like the [PowerSwitch Tail ](http://www.powerswitchtail.com/)($25 each), also, they are wireless with a pretty good range as well.

[![](http://mitchtech.net/wp-content/uploads/2012/05/3pk-outlet-dx-300x225.jpg)](http://mitchtech.net/android-ioio-remote-outlets/3pk-outlet-dx/)

They also have [single](http://dx.com/p/wireless-remote-controlled-ac-power-adapter-set-110v-us-plug-59269?Utm_rid=33954493&Utm_source=affiliate) and [dual](http://dx.com/p/2-channel-wireless-remote-controlled-ac-power-adapters-set-110v-us-plug-82400?Utm_rid=33954493&Utm_source=affiliate) outlet version. Note: all three of these models are 110V/US plugs.

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

  * 3 Channel Remote AC outlet (available at [DealExtreme](http://dx.com/p/3-channel-wireless-remote-controlled-ac-power-adapters-set-110v-us-plug-82399?Utm_rid=33954493&Utm_source=affiliate))

  * 6x NPN 2N3904 transistor

  * 6x 10k ohm resistor

  * Breadboard

  * Power supply

  * Hook-up wire

#### Assembly

First, remove the outer plastic case from the remote controller. Looking at the board with the button side facing up, locate the seven solderable holes in the circuit board.  Six correspond to each button (on/off for each outlet) and the seventh is the common line.  Connecting any of the button lines to the common line will activate the connection, turning on or off the respective switch.  Solder a wire to each of the switches and the common line:

[![](http://mitchtech.net/wp-content/uploads/2012/05/remote-solder-300x225.jpg)](http://mitchtech.net/android-ioio-remote-outlets/remote-solder/)

Connect each button line to the collector of a transistor and the emitter to the common line.  Connect the base of the transistor to the desired IOIO pin with a 10k ohm resistor in series. Finally, connect the former terminals for the battery of the remote to +3.3v and GND on the IOIO. Here is a diagram of the completed circuit (created with [Fritzing](http://fritzing.org/)):

[![](http://mitchtech.net/wp-content/uploads/2012/05/ioio_remote_ac_outlets.png)](http://mitchtech.net/wp-content/uploads/2012/05/ioio_remote_ac_outlets.png)

And here is a picture of the completed circuit:

[![](http://mitchtech.net/wp-content/uploads/2012/05/power-outlet-breadboard-300x225.jpg)](http://mitchtech.net/android-ioio-remote-outlets/power-outlet-breadboard/)

## Software

#### Get the source

With the circuit assembled, the next step is to get the demo application on the Android device. You can either [download the pre-built .apk](http://mitch-tech.appspot.com/ioio/IOIORemoteOutlets.apk) or checkout the source from [Github](https://github.com/mitchtech/android_ioio_accelerometer_servos):

```
git clone git://github.com/mitchtech/android_ioio_remote_outlets.git
```

If you are building from source, you will also need to import the IOIO Library project, and optionally the IOIO Bluetooth library projects, both available [here](https://github.com/ytai/ioio):

```
git clone git://github.com/ytai/ioio.git
```

#### Install, connect, profit!

Finally, upload the app to the Android device (or browse to this page on the device and download the apk above). Connect the device to the IOIO, and start up the app.

