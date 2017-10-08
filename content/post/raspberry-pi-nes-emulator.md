+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-14 23:50:50+00:00"
excerpt = "This tutorial will demonstrate how to install Nintendo NES/Famicom emulator on the Raspberry Pi running Debian"
slug = "raspberry-pi-nes-emulator"
tags = ["ARM","Emulator","Famicom","Linux","NES","Nintendo","Raspberry Pi","USB"]
title = "Raspberry Pi NES Emulator"

+++

![](/img/pi-nes-emulator-mario3.png)

This tutorial will demonstrate how to install Nintendo NES/Famicom emulator on the Raspberry Pi running Debian.  Begin by installing the necessary dependencies. In a terminal, enter:

```
sudo apt-get install scons libsdl1.2-dev libsdl1.2debian-esd subversion libgtk2.0-dev
```

Checkout the most recent sources using subversion:

```
<del>svn checkout https://fceultra.svn.sourceforge.net/svnroot/fceultra/fceu fceultra</del>
```

The repo has moved here:

```
svn checkout svn://svn.code.sf.net/p/fceultra/code/fceu fceultra
```

Change directory into the root of the source tree

```
cd fceultra/
```

Compile and install FCEU using the scons build tool:

```
sudo scons GTK=1 install
```

That's it! To run:

```
fceux
```

Then select the ROM with from the title bar menu, File->Open ROM, or with Ctrl+O.

![](/img/pi-nes-emulator-mario3-full.png)

You can easily setup a gamepad too, like the [USB NES RetroPort](http://www.retrousb.com/product_info.php?cPath=21&products_id=28). This adapter converts an authentic NES controller to USB.   To configure, run fceux using the inputcfg flag to setup configure.  Press the corresponding buttons in series as they are prompted. Note: There are two dashes ( - - ) together in the command below:

```
fceux --inputcfg gamepad1
```

![](/img/pi-nes-controller.jpg)

