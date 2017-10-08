+++
author = "michael"
categories = ["Tutorials","Ubuntu"]
comments = true
date = "2012-05-02 15:45:46+00:00"
slug = "mult-axis-google-earth-controller"
tags = ["3D Connection","Device Driver","Google Earth","Joystick","Linux","Multi-axis","SpaceNavigator","Ubuntu"]
title = "Google Earth + Mult-axis Controller"
banner = "https://img.youtube.com/vi/xR3xUYtjg5Y/0.jpg"

+++

{{< youtube xR3xUYtjg5Y >}}

Six degree of freedom control for Google Earth using the 3Dconnexion SpaceNavigator on Ubuntu Linux.  Based on directions from here: [http://code.google.com/p/liquid-galaxy/wiki/LinuxSpaceNavigator](http://code.google.com/p/liquid-galaxy/wiki/LinuxSpaceNavigator)

First, install the necessary package dependencies:

```
sudo apt-get install xinput xserver-xorg-input-joystick
```

Next we add a udev rule to automatically recognize the Space Navigator based on its vendor/product ids and create a symlink at /dev/input/spacenavigator. Create the following file as root:

```
sudo gedit /etc/udev/rules.d/90-spacenavigator.rules
```

and add the following line:

```
`KERNEL=="event[0-9]*", SYSFS{idVendor}=="046d", SYSFS{idProduct}=="c62[68]", MODE="0664", GROUP="plugdev", SYMLINK+="input/spacenavigator"
````

NOTE: This appears to be multiple lines, but should be copied as a single line; udev rules cannot span multiple lines.

Next, we must modify the drivers.ini file to add support for google earth. This file may in exist in several locations depending on how you installed Google Earth. If you installed as root, edit the driver file here. Note: may also be located at /opt/google-earth/drivers.ini depending on software version.

```
sudo gedit /opt/google/earth/free/drivers.ini
```

If you installed Google Earth as your local user, edit the driver file here:

```
gedit ~/.googleearth/drivers.ini
```

Add the following lines to the SETTINGS stanza of the drivers.ini. Note: these paramaters can be manipulated to suit your own needs. The ‘gutter’ paramater is particularly useful as it defines the ‘dead zone’ around the center axis.

```
; Settings for multi-axis controllers
SpaceNavigator/sensitivityX = 0.125
SpaceNavigator/sensitivityY = 0.125
SpaceNavigator/sensitivityZ = 0.030
SpaceNavigator/sensitivityPitch = 0.01
SpaceNavigator/sensitivityYaw = 0.004
SpaceNavigator/sensitivityRoll = 0.007
SpaceNavigator/device = /dev/input/spacenavigator
SpaceNavigator/zeroX = 0.0
SpaceNavigator/zeroY = 0.0
SpaceNavigator/zeroZ = 0.0
SpaceNavigator/zeroPitch = 0.0
SpaceNavigator/zeroYaw = 0.0
SpaceNavigator/zeroRoll = 0.0
SpaceNavigator/gutterValue = 0.1
```

At this point the drivers should be fully functional for use with Google Earth. However, your OS may indentify the SpaceNvigator as a mouse, making control somewhat awkward. You can disable this behavior using the xinput set-int-prop command:

```
xinput set-int-prop "3Dconnexion SpaceNavigator" "Device Enabled" 8 0
```

The same command can also be used to re-enable the mouse behavior:

```
xinput set-int-prop "3Dconnexion SpaceNavigator" "Device Enabled" 8 1
```

