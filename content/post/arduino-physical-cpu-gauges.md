---
author: michael
comments: true
date: 2012-07-03 14:46:30+00:00
layout: post
link: http://mitchtech.net/arduino-physical-cpu-gauges/
slug: arduino-physical-cpu-gauges
title: Arduino Physical CPU Gauges
categories:
- Arduino
- Tutorials
- Ubuntu
tags:
- Analog Output
- Arduino
- CPU
- DIY
- Electronics
- Gauge
- Linux
- Memory
- Meter
- Microcontroller
- Physical Notifier
- Python
- Serial
- Servo
- Ubuntu
- USB
---

{{< youtube xQ5s0xv4ies >}}

Use Arduino and two hobby servos to control physical servo gauges for cpu activity, memory usage, bandwidth, and more. The script uses the python [psutil](http://code.google.com/p/psutil/) and [pyserial](http://pyserial.sourceforge.net/) modules. The psutil module provides an interface for retrieving information on all running processes and system utilization (CPU, disk, memory, network) providing service similar to command line tools such as ps, top, iostat, and netstat. The servo control portion of the project is based on [Arduino-Python 4-Axis Servo Control](http://principialabs.com/arduino-python-4-axis-servo-control/)by Brian Wendt, and the Arduino sketch is essentially unmodified from the [SerialServoControl Sketch on Sparkfun.](http://www.sparkfun.com/tutorials/304)

## Hardware

Connect the red, power lines of the servos to +5v, the black ground lines to GND, and the yellow signal lines to the desired output pins, 5 and 6 in the example (others can be used, but must be PWM capable

[![](http://mitchtech.net/wp-content/uploads/2012/07/arduino_dual_servo.png)](http://mitchtech.net/arduino-physical-cpu-gauges/arduino_dual_servo/)

You can download my cheesy gauge overlay from here:

```
http://mitchtech.net/arduino-physical-cpu-gauges/gauges/
```

Print it out, cut out the gauges, and poke a hole in the lower center of the gauge.  Remove the servo horn, slide the shaft through the hole in the gauge printout, and reconnect the servo horn on top of it.

## Software

The first step is to install the python psutil and pyserial modules. The easiest way to install it is using the python pip package manager. If you don't have it installed already, you can install it using apt-get:

```
sudo apt-get install python-pip
```

Then install the psutil and pyserial modules:

```
sudo pip install psutil pyserial
```

Next, flash the sketch to the Arduino board. You can download it or copy and paste into the Arduino IDE.

{{< gist mitchtech 3029316 >}}

Then download or copy and paste the Python script:

{{< gist mitchtech 3029096 >}}

That's it! To run the script:

```
python  cpu_serial_servo.py
```

Note: If you receive this error:

```
raise SerialException("could not open port %s: %s" % (self._port, msg)) serial.serialutil.SerialException: could not open port /dev/ttyUSB0: [Errno 13] Permission denied: '/dev/ttyUSB0'
```

The problem is the default permissions of the /dev/ttyUSB0 (or /dev/ttyACM0) device. This can be fixed by running the command:

```
sudo chmod 777 /dev/ttyUSB0
```

