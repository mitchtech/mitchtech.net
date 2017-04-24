+++
author = "michael"
categories = ["Kinect","Tutorials","Ubuntu"]
comments = true
date = "2012-05-02 05:08:22+00:00"
slug = "ubuntu-openkinect"
tags = ["Hack","Kinect","Linux","OpenKinect","Ubuntu"]
title = "Ubuntu + OpenKinect"

+++

{{< youtube gQEAueuF0Ig >}}

#### Getting started with OpenKinect on Ubuntu Linux

There are two ways you can get OpenKinect (freenect) working on Ubuntu: either by installing the prebuilt PPA package, or compiling from source.  I’ve confirmed at both of these methods are functional, the package based method is slightly more straightforward, and allows updates from the apt package manager. This article will demonstrate installation via this method, for details on the manual compilation method, check out the official [OpenKinect Getting Started Guide](http://openkinect.org/wiki/Getting_Started#Ubuntu)

#### Quickstart

```
sudo add-apt-repository ppa:floe/libtisch

sudo apt-get update

sudo apt-get install libfreenect libfreenect-dev libfreenect-demos

sudo freenect-glview
```

#### Steps Explained

For those unfamiliar, Ubuntu allows developers to create and distribute their own software packages, called [Launchpad Personal Package Archives (PPA)](https://help.launchpad.net/Packaging/PPA). To use one, the package needs to be added to the apt repository list, in this case:

```
sudo add-apt-repository ppa:floe/libtisch
```

This adds the repo, but doesn’t update the apt package list. Thus, we must resynch it:

```
sudo apt-get update
```

Then, install libfreenect, the development headers, and the demo apps:

```
sudo apt-get install libfreenect libfreenect-dev libfreenect-demos
```

You can run it as root:

```
sudo freenect-glview
```

To run in user mode, you need to add yourself to the UNIX ‘video’ group and log back in (The package includes udev daemon rules allowing access to the group video).

```
sudo adduser $USER video
```

Then log out and back in. Reboot is not necessary, just plug cycle the Kinect (if already connected, unplug and plug back in). Then run the demo app:

```
freenect-glview
```

How the Kinect is actually working
Here’s another video, this one taken under infrared of my IP camera. It demonstrates how the infrared projector of the Kinect works.

{{< youtube C-Xlkb1MU4I >}}

