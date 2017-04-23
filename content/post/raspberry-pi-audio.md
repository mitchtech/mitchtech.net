---
author: michael
comments: true
date: 2012-06-02 18:42:33+00:00
layout: post
link: http://mitchtech.net/raspberry-pi-audio/
slug: raspberry-pi-audio
title: Raspberry Pi Audio
categories:
- Raspberry Pi
- Tutorials
tags:
- ARM
- Audio
- Linux
- Raspberry Pi
---

[![](http://mitchtech.net/wp-content/uploads/2012/06/pi-usb-drive-300x225.jpg)](http://mitchtech.net/raspberry-pi-audio/pi-usb-drive/)

Currently, the audio drivers for the Raspberry Pi are still in beta, and as such come disabled in the standard release (debian6-19-04-2012.zip). Here's a quick way to get it up and running for both the HDMI as well as the analog output. Open up a terminal and install the alsa (Advanced Linux Sound Architecture) utility package:

```
sudo apt-get install alsa-utils
```

Now load the sound driver using modprobe:

```
sudo modprobe snd_bcm2835
```

By default output will be automatic (HDMI if supported, else analog). You can force it to use a specific interface with:

```
sudo amixer cset numid=3
```

Substituting <n> for the desired mode: 0=auto, 1=headphones, 2=hdmi. For example, to force the Raspberry Pi to use the analog output:

```
sudo amixer cset numid=3 1
```

