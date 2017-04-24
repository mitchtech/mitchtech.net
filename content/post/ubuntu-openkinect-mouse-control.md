+++
author = "michael"
categories = ["Kinect","Tutorials","Ubuntu"]
comments = true
date = "2012-05-02 05:12:13+00:00"
layout = "post"
link = "http://mitchtech.net/ubuntu-openkinect-mouse-control/"
slug = "ubuntu-openkinect-mouse-control"
tags = ["Hack","Kinect","Linux","OpenKinect","Ubuntu"]
title = "Ubuntu + OpenKinect + Mouse Control"

+++

{{< youtube y56YDc65kRo >}}

#### Mouse control with OpenKinect on Ubuntu Linux

Here is a quick tutorial to get use your hand as a mouse in a Minority Report-esque interface using the Kinect and Ubuntu.  Credit to [Ooblik (Tim Flaman)](https://github.com/Ooblik) for the awesome project. Before you begin, ensure that you have [installed the OpenKinect drivers](http://mitchtech.net/ubuntu-openkinect/) and they are functioning correctly.

#### Quickstart

```
sudo apt-get install libncurses5-dev freeglut3-dev libX11-dev libxtst-dev libxmu-dev cmake git

git clone https://github.com/Ooblik/Kinect-Mouse.git

cd Kinect-Mouse

mkdir build

cd build

cmake ..

make

sudo ./kmouse
```

#### Steps explained:

Install a few dependencies for the Kinect mouse:

```
sudo apt-get install libncurses5-dev freeglut3-dev libX11-dev libxtst-dev libxmu-dev cmake git
```

Use git to clone the source from Ooblik’s repo on Github:

```
git clone https://github.com/Ooblik/Kinect-Mouse.git
```

Then make yourself a build directory within the repo, use cmake to configure, and make to build.

```
cd Kinect-Mouse

mkdir build

cd build

cmake ..

make
```

Ensure that your Kinect is plugged in (USB and power), and run kmouse. It needs to be run as root unless you have followed the steps here to add your user to the ‘video’ group.

```
sudo ./kmouse
```

You will likely need to reposition the Kinect (or yourself) to get it working accurately… The mouse only works at a very specific distance from the Kinect.  This is the red area in the video viewer. To click the mouse, remain still over the target and the mouse will left click. Interaction is little more than a proof of concept at present… but it works!

