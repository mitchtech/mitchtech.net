+++
author = "michael"
categories = ["Android","Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-02 18:17:32+00:00"
slug = "vnc-setup-on-raspberry-pi-from-android"
tags = ["ARM","Linux","Raspberry Pi","SSH","Ubuntu","VNC"]
title = "VNC setup on Raspberry Pi from Android"
banner = "img/nexus-pi-vnc.jpg"

+++

![](/img/nexus-pi-vnc.jpg)

This tutorial will demonstrate how to setup and connect to a Raspberry Pi over VNC from Android. This process assumes you have Debian for Raspberry Pi installed on an SD card. If not, see [RPi Easy SD card setup](http://elinux.org/RPi_Easy_SD_Card_Setup). It also assumes that you have a display connected to the Raspberry Pi. If you don't have a display available, the steps to configure VNC remotely are outlined in my last tutorial: [VNC setup on Raspberry Pi from Ubuntu](http://mitchtech.net/vnc-setup-on-raspberry-pi-from-ubuntu/)

#### Getting the IP address of the Raspberry Pi

The first step is to locate the Raspberry Pi on your network. Open up a terminal on the Raspberry Pi and type:

```
ifconfig
```

All the network interface configurations will be displayed, including the IP address. Make a note of this, it will be needed later.

#### Configuring VNC

Next, we need to install the VNC server. In a terminal on the Pi type:

```
sudo apt-get install tightvncserver
```

Now, start the VNC server on the Raspberry Pi. Adjust the geometry paramater to your desired display size. 1200x720 works well for the Galaxy Nexus (image above) and the Xoom (image below):

```
vncserver :1 -geometry 1200x720 -depth 16 -pixelformat rgb565
```

You will be prompted to create a password for VNC login. Once you do, you should see a line looking something like this:

```
New 'X' desktop is raspberrypi:1
```

#### Connecting from Android

You will need to download any VNC client to connect to the Raspberry Pi VNC session. I use androidVNC, but any VNC client should work as long as the settings are correct:

```
Nick : pi (or whatever you want)
address : your_ip_address
port : 5901
password : your_password
Touch Mouse; D-Pad Pan; Mouse pointer
control mode: TouchPad
```

Be sure to replace your_ip_address and your_password with your own settings.

![](/img/xoom-pi-vnc.jpg)

