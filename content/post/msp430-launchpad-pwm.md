---
author: meyers
comments: true
date: 2012-07-09 23:06:03+00:00
excerpt: How to perform pulse width modulation using a MSP430g2553 TI Launchpad to
  control a sparkfun servo motor.
layout: post
link: http://mitchtech.net/msp430-launchpad-pwm/
slug: msp430-launchpad-pwm
title: MSP430 Launchpad + PWM
categories:
- MSP430 Launchpad
- Tutorials
tags:
- Arduino
- launchpad
- msp430
- pulse width modulation
- PWM
- Servo
---

[![](http://mitchtech.net/wp-content/uploads/2012/06/msp430+servo-300x225.jpg)](http://mitchtech.net/msp430-launchpad-pwm/samsung/)

Inspired by [this](http://gushh.net/blog/?cat=361) tutorial.

The following tutorial will describe how perform pulse width modulation using a MSP430g2553 TI Launchpad to control a sparkfun servo motor.

## Prerequisites

Please see [Cross-Compiling for TI MSP430 Launchpad](http://mitchtech.net/cross-compiling-for-ti-msp430-launchpad/) to setup your development environment.

## Hardware

  * Servo motor

  * MSP430

  * Power

I'm using the Arduino to power the servo motors.  Alternatively you may use USB, a wall plug, or a battery.  The MSP430 is being used to generate the PWM for control.

Connect your servo control wire to MSP430 pin P1.2.

## Software

Save the below code as pwm.c
{{< gist mitchtech 3024004 >}}

Compile install and run the code!

```
sudo mspdebug rf2500
erase
prog pwm.elf
run
```

If your lucky then your device will have moved a bit and you might notice that the device didn't reach its full range of motion.  You will need to play with the SERVO_MIN and SERVO_MAX constants to achieve the devices full range of motion.
{{< youtube BPEImNC2fT0 >}}

## Debugging

This section contains hints and debug strategies if things didn't just magically work for you.

#### Header File

The biggest trouble I had was getting the correct header file. An incorrect header file did not produce any warnings.  The only feedback for a header file that didn't match my board was the device moving less than 1 degree and behaving non-deterministic.  Look at the documentation that came with your board to find the exact device. A list of device headers can be found in the directory /usr/msp430/include/.

#### Erase

The mspdebug program hosts a suite of commands.  A list of commands can be gotten by typing help.  The erase command is one that I found late into the night. Be sure to issue the erase command before you issue the load command.

#### Is it broke?

Often times when things aren't working you will wonder if you broke the board because you touched some pin, got pissed off and threw it across the room, or your kitty cat Mr. Bigglesworth played kitty frisbee with it.  Regardless of the reason you want some feedback that the board is still alive.  I like to reload a piece of code that blinks the development board built-in lights [LED blinking tutorial](http://mitchtech.net/cross-compiling-for-ti-msp430-launchpad/).

