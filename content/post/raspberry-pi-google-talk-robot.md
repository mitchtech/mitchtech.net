+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2013-01-17 02:06:48+00:00"
slug = "raspberry-pi-google-talk-robot"
tags = ["ARM","Digital Input","Digital Output","DIY","Electronics","Google Talk","GPIO","Home Automation","Linux","Microcontroller","Raspberry Pi","XMPP"]
title = "Raspberry Pi Google Talk Robot"

+++

{{< youtube vd6RlkAXWRs >}}

Google Talk/Chat/Messenger is normally used by humans to interact with other humans. However, its underlying technology can also be used as a mechanism to implement software robots.  Internet bots, also known as web robots, WWW robots or simply 'bots' can also utilize the technology to perform automated functions over the web.  There are many such bots in existence, offering a diverse spectrum of services from jokes (jokes@askme.im) to URL Shortening using bit.ly (url@askme.im), even mathematical calculation (math@bot.im).  Using such bots is quick and easy to configure, all that must be done is to add the bot as a contact to your messaging account.  Then, whenever you desire data from the service, simply text the command to the bot and it will respond with the respective message.

The Raspi Bot is essentially the same as any other automated Internet robot.  To configure it, it must first have its own e-mail address associated with a Google talk account.  This e-mail address must also be added as a contact with the account that wishes to communicate to the bot.  Then, whenever the script is running on the remote machine, it will log into Google chat and appear as a friend in your contact list.

The software itself is essentially just a Python daemon script that is a wrapper around the XMPP protocol.  When executed, the script will sign in to Google talk using its own username and password.  The Python script is derived from the open source project pygtalkrobot: An open source python gtalk(google talk) bot framework using XMPPPY and PyDNS libraries, that also references the source code of python-jabberbot.

### Software

The Raspi Bot requires several additional Python modules for use.  The easiest way to install these is with the python pip package manager. If you don't have it installed, you can install them using apt-get:

```
sudo apt-get install python-pip git-core python2.7-dev
```

Then update the easy_install index:

```
sudo easy_install -U distribute
```

And install the GPIO, xmpppy, and pydns modules:

```
sudo pip install RPi.GPIO xmpppy pydns
```

Then clone my repo for the Raspi Gtalk robot:

```
git clone https://github.com/mitchtech/raspi_gtalk_robot.git
```

Now change into the newly created directory:

```
cd raspi_gtalk_robot
```

Finally, you will need  to configure the Raspi Bot’s Gtalk username and password.  This is done by editing the fields BOT_GTALK_USER, BOT_GTALK_PASS, and BOT_ADMIN, on lines 31-33 in the raspiBot.py file.  It is recommended, though not required, to give the Raspi Bot its own Gmail account. Since access to the Raspberry Pi GPIO pins is restricted, the script needs to be run with sudo:

```
sudo python ./raspiBot.py
```

This basic sample script supports the following commands:

  * [pinon|pon|on|high] [pin] : turns on the specified GPIO pin

  * [pinoff|poff|off|low] [pin] : turns off the specified GPIO pin

  * [write|w] [pin] [state] : writes specified state to the specified GPIO pin

  * [read|r] [pin]: reads the value of the specified GPIO pin

  * [available|online|busy|dnd|away|idle|out|xa] [arg1] : set gtalk state and status message to specified argument

  * [shell|bash] [arg1] : executes the specified shell command argument after 'shell' or 'bash'

For example, sending the message "pinon 10" will turn on GPIO pin #10, "read 8" will read the current state of GPIO pin 8, or "bash ps" to execute the shell command 'ps'.

### Hardware

The video demonstration uses a slide switch connected to GPIO pin 8 and an LED connected to GPIO pin 10.  Here is a diagram of how this is wired   (created with [Fritzing](http://fritzing.org/)):

[![raspi_gtalk_robot](http://mitchtech.net/wp-content/uploads/2013/01/raspi_gtalk_robot-300x277.png)](http://mitchtech.net/raspberry-pi-google-talk-robot/raspi_gtalk_robot/)

#### Use case #1: Home automation

One of the most obvious usages of this technology is for home automation purposes. The Raspi Bot can be accessed anywhere with Google talk, which to my understanding, is nearly every system in existence.  Send the Raspi Bot messages to turn on and off lights and other electrical appliances.

This is also useful to provide immediate notification in the event of intrusion detection. The Raspi Bot can be supplemented with additional security sensors, including infrared motion, and ultrasonic distance sensors. If any pre-programmed sensor violates any predefined condition, you can be immediately notified via message from the Raspi Bot.

#### Use case #2: Remote shell

The Raspi Bot can be used essentially as a remote shell.  In this configuration, every message sent to the Raspi Bot will be interpreted as a shell command with the output piped back to the user in the form of a response message.  Obviously, this could raise some security concerns. To protect against misuse, the Raspi Bot will only respond to Google chat messages from the Google user designated as the administrator of the bot.  By default, messages from any other user will simply be ignored.

The following is a small subset of the relatively benign commands possible to be run remotely via the Raspi Bot:

  * vmstat - system activity, hardware and information

  * uptime - how long the system has been running

  * w - logged in users and their process activity

  * ps - reports a snapshot of the current processes

  * free - physical and swap memory usage

  * iostat - average CPU load, disk activity

Arguably, disclosure of any amount of information about system can be considered a security issue such as that reported by some of the above tools.  For users more concerned about convenience over security exposure, much more elaborate commands can be run, such as executing additional scripts or accessing private data.

#### Use case #3: Remote Reboot

Another problem that can be solved by the Raspi Bot is frozen remote machines. We've all been there before, attempting to access a remote machine only to find it to be completely non-responsive to any form of remote login.  These cases, we (or maybe a system administrator somewhere) would usually have to make a trip to the physical location of the server and push ‘the big red button’ to reboot the affected machine.  The situation can be eliminated completely by deputizing a Raspi Bot as a remote reboot agent. This can be done by adding bot controlled relay(s) to the power supplies of the machines.  In the event any of the machines controlled by the Raspi Bot becomes non-responsive, simply send the appropriate Google talk message to flip the respective relay, and reboot the affected machine.  Here's a diagram of how this would look:

[![raspi_remote_reboot](http://mitchtech.net/wp-content/uploads/2013/01/raspi_remote_reboot-300x181.png)](http://mitchtech.net/raspberry-pi-google-talk-robot/raspi_remote_reboot/)

