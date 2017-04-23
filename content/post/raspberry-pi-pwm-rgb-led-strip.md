---
author: michael
comments: true
date: 2013-01-15 23:29:15+00:00
layout: post
link: http://mitchtech.net/raspberry-pi-pwm-rgb-led-strip/
slug: raspberry-pi-pwm-rgb-led-strip
title: Raspberry Pi + PWM RGB LED Strip
categories:
- Raspberry Pi
- Tutorials
tags:
- ARM
- Device Driver
- DIY
- Electronics
- Home Automation
- Kernel
- LED
- Linux
- Microcontroller
- PWM
- Raspberry Pi
- RGB LED Strip
---

{{< youtube --d8Sp2yoUU >}}

This tutorial demonstrates how to easily use a Raspberry Pi to drive 12V RGB LED strips using Pulse Width Modulation (PWM).  Out of the box, the Raspberry Pi has only one GPIO pin that is capable of pulse width modulation (PWM).  However, thanks to the efforts of [Richard Hirst and his servoblaster kernel module](https://github.com/richardghirst/PiBits/tree/master/ServoBlaster), standard GPIO pins can be used to perform PWM.

Note: The flashing of the LED strip due to PWM is only noticeable in the uploaded video; in reality, the colors progress smoothly without any visible flashing.

## Hardware

#### Parts needed:

  * Raspberry Pi

  * 3 x TIP120 power transistors

  * RGB LED strip

  * Perfboard/Breadboard

  * Hook-up wire

#### Assembly

Connect a 12V power supply to the 12V pad on the RGB LED strip, connect the base of each TIP120 power transistor to its respective GPIO pin (pins 18, 23, and 24 in this example), connect the collector of each to its matching pad on the LED strip, and finally, connect the emitters to common ground for both the Raspberry Pi and the 12V power supply. Here is a diagram of the circuit  (created with [Fritzing](http://fritzing.org/)):

[![raspi_rgb_led](http://mitchtech.net/wp-content/uploads/2013/01/raspi_rgb_led-300x194.png)](http://mitchtech.net/raspberry-pi-pwm-rgb-led-strip/raspi_rgb_led/)

## Software

#### Configure servoblaster.

The next step is to configure the servoblaster kernel driver. The driver creates a device file, /dev/servoblaster to which commands can be sent to control the servos. The commands take the form "=" with servo number representing the desired servo (0-7 in this case) and servo position representing the pulse width in units of 10 µs. For example, to send servo 3 a pulse width of 120 µs:

```
echo 3=120 > /dev/servoblaster
```

To setup the servo blaster on the Raspberry Pi, we will need to have git installed to pull down the sources. If you don't have it installed already, open a terminal and run:

```
sudo apt-get install git-core
```

Then pull down the sources from Richard’s Github repo:

```
git clone https://github.com/richardghirst/PiBits.git
```

Now change into the servo blaster directory:

```
cd PiBits/ServoBlaster
```

And compile and install the module:

```
make install_autostart
```

This command also sets up the necessary udev rules for accessing the /dev/servoblaster device. Note: using the ’install_autostart ’ command will set up a raspberry pi to load the servo blaster kernel module on every boot. If you don't want this behavior, execute ‘make install’ instead. In either case, the module will not yet be loaded so go ahead and install it using modprobe:

```
sudo modprobe servoblaster
```

#### Sample code usage.

Now that all the prerequisites have been installed and the servo blaster device configured, on to the actual sample code. The python sample script uses PWM to fade from blue to violet, to red, to yellow, to green, to teal, back to blue.

{{< gist mitchtech 4543601 >}}

