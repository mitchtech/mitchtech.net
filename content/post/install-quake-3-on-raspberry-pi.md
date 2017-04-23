---
author: michael
comments: true
date: 2012-06-02 18:17:37+00:00
layout: post
link: http://mitchtech.net/install-quake-3-on-raspberry-pi/
slug: install-quake-3-on-raspberry-pi
title: Install Quake 3 on Raspberry Pi
categories:
- Raspberry Pi
- Tutorials
tags:
- ARM
- Game
- Linux
- Quake3
- Raspberry Pi
- Ubuntu
---

[![](http://mitchtech.net/wp-content/uploads/2012/06/pi-quake3-intro-300x225.jpg)](http://mitchtech.net/install-quake-3-on-raspberry-pi/pi-quake3-intro/)

Here is the easiest possible way to install Quake 3 on the Raspberry Pi with [debian6-19-04-2012.](http://downloads.raspberrypi.org/images/debian/6/debian6-19-04-2012/debian6-19-04-2012.zip)  Just copy and paste the following in a terminal on the Pi:

```
cd ~
wget http://radium.hexxeh.net/quake3.zip
wget http://www.andershizzle.com/Q3%20Demo%20Paks.zip
unzip quake3.zip
unzip Q3\ Demo\ Paks.zip
rm quake3.zip
rm Q3\ Demo\ Paks.zip
mv ./baseq3/pak* ./quake3/baseq3/
rm -rf ./baseq3/
chmod +x /home/pi/quake3/start.sh
chmod +x /home/pi/quake3/ioquake3.arm
chmod +x /home/pi/quake3/ioq3ded.arm
```

Note: After reports of connection issues with the downloads, I have hosted mirror versions of the two files here:

```
wget http://dl.dropbox.com/u/1816557/quake3.zip
wget http://dl.dropbox.com/u/1816557/Q3%20Demo%20Paks.zip
```

To start quake3, switch to the install directory, and execute the start.sh script in a terminal:

```
cd ~/quake3/
./start.sh
```

[![](http://mitchtech.net/wp-content/uploads/2012/06/pi-quake3-gameplay-300x225.jpg)](http://mitchtech.net/install-quake-3-on-raspberry-pi/pi-quake3-gameplay/)

