+++
author = "michael"
categories = ["Raspberry Pi","Tutorials","Ubuntu"]
comments = true
date = "2012-06-02 18:02:48+00:00"
layout = "post"
link = "http://mitchtech.net/vnc-setup-on-raspberry-pi-from-ubuntu/"
slug = "vnc-setup-on-raspberry-pi-from-ubuntu"
tags = ["ARM","Linux","Raspberry Pi","SSH","Ubuntu","VNC"]
title = "VNC setup on Raspberry Pi from Ubuntu"

+++

{{< youtube KuICf0nlb-c >}}

This tutorial will demonstrate how to setup and connect to a Raspberry Pi over VNC from Ubuntu. This process is easier if you have a display connected to the Raspberry Pi, but will also show the steps to connect with only Ethernet and power connected. It assumes you have Debian for Raspberry Pi installed on an SD card. If not, see [RPi Easy SD card setup](http://elinux.org/RPi_Easy_SD_Card_Setup)

#### Getting the IP address of the Raspberry Pi

The first step is to locate the Raspberry Pi on your network. If you have access to a display for your Raspberry Pi, this task is simple, in a terminal simply type:

```
ifconfig
```

All the network interface configurations will be displayed, including the IP address. However, if you don't have a display for your Raspberry Pi, this isn't an option. For this task, we can use the Linux nmap (Network Mapper) utility.

```
sudo apt-get install nmap
```

Then run a scan on your local network. Be change to the specifics of your own network.

```
nmap -sV -p 22 192.168.0.1-255
```

The results will display every machine that could be identified on port 22. The Raspberry Pi (running Debian) looks something like this:

```
Nmap scan report for 192.168.0.112
Host is up (0.033s latency).
PORT STATE SERVICE VERSION
22/tcp open ssh OpenSSH 5.5p1 Debian 6+squeeze2 (protocol 2.0)
Service Info: OS: Linux
```

#### Connecting over SSH

So we know that the Raspberry Pi has IP address: 192.168.0.112. Now we can ssh to it:

```
ssh pi@192.168.0.112
```

And you should receive a message like this:

```
The authenticity of host '192.168.0.112 (192.168.0.112)' can't be established.
RSA key fingerprint is xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx.
Are you sure you want to continue connecting (yes/no)?
```

Type yes at the prompt, then enter the password for the user pi, 'raspberry' by default. You should get a prompt that looks like this:

```
pi@raspberrypi:~$
```

#### Configuring VNC

Now that we have logged in to the Raspberry Pi, we can setup VNC for remote access. First we need to install the VNC server:

```
sudo apt-get install tightvncserver
```

Next, start the VNC server on the Raspberry Pi. Adjust the geometry paramater to your desired display size.

```

vncserver :1 -geometry 1024x600 -depth 16 -pixelformat rgb565
>
>

```

You will be prompted to create a password for VNC login. Once you do, you should see a line looking something like this:

```
New 'X' desktop is raspberrypi:1
```

Now, we can finally connect to the Pi with VNC. Back on the Ubuntu machine, install the VNC viewer client:

```
sudo apt-get install xtightvncviewer
```

Then connect to the running VNC server:

```
vncviewer 192.168.0.112:5901
```

To stop the VNC viewer, just close the application. To stop the VNC server, issue the following command (on the Raspberry Pi):

```
vncserver -kill :1
```

[![](http://mitchtech.net/wp-content/uploads/2012/06/ubuntu-pi-vnc-300x187.png)](http://mitchtech.net/vnc-setup-on-raspberry-pi-from-ubuntu/ubuntu-pi-vnc/)
