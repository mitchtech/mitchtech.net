+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-29 04:20:47+00:00"
excerpt = "This tutorial will demonstrate how to easily turn your Raspberry Pi into a physical Gmail notifier, in only 10 lines of python!"
slug = "raspberry-pi-physical-gmail-notifier"
tags = ["ARM","Cron","Digital Output","DIY","Electronics","Gmail","GPIO","LED","Linux","Microcontroller","Physical Notifier","Python","Raspberry Pi"]
title = "Raspberry Pi Physical Gmail Notifier"
banner = "img/pi-physical-gmail-notifier.jpg"

+++

![](/img/pi-physical-gmail-notifier.jpg)

This tutorial will demonstrate how to easily turn your Raspberry Pi into a physical Gmail notifier, in only 10 lines of python! If the configured Gmail account has unread messages, the LED will be illuminated, otherwise dim.  The project was inspired by the [Arduino/Mac version by J4mie](http://j4mie.org/blog/how-to-make-a-physical-gmail-notifier/) adapted for use on the Raspberry Pi.

Here is a diagram of the wiring of the LED with a 330 ohm resistor in series (created with [Fritzing](http://fritzing.org/)):

![raspi_gmail_led](/img/raspi_gmail_led.png)

The python script uses the [feedparser module](http://code.google.com/p/feedparser/) to simplify interaction with Gmail and the RPi.GPIO module to control the GPIO pins. The easiest way to install these is using the python pip package manager. If you don't have it installed, you can install the pip package manager using apt-get. In a terminal on the Pi:

EDIT: For [2012-07-15-wheezy-raspbian.zip](http://downloads.raspberrypi.org/images/raspbian/2012-07-15-wheezy-raspbian/2012-07-15-wheezy-raspbian.zip) and newer, the Python development headers (python2.7-dev) are also required:

```
sudo apt-get install python-pip python2.7-dev
```

Next, for pip to work correctly you will need to update to a newer version of distribute using easy_install:

```
sudo easy_install -U distribute
```

Then install the feedparser and GPIO modules with pip:

```
sudo pip install feedparser RPi.GPIO
```

Once the pre-requisites have been installed, download , or copy and paste the following Python script to the Raspberry Pi:

{{< gist mitchtech 3015384 >}}

The final step is to configure the script to run every minute as a cron job. To do so, open the global crontab for editing:

```
sudo crontab -e
```

Then add this line to the end of the file (adjust to the location of the python script):

```
* * * * * python /home/pi/raspi_gmail.py
```

That's it! From now on, cron will execute the script once every minute.  If you have unread messages, the GPIO pin will be pulled high, lighting the LED, otherwise, it will be disabled, dimming the LED.

