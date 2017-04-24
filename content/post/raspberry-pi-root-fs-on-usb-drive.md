+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-14 00:49:07+00:00"
layout = "post"
link = "http://mitchtech.net/raspberry-pi-root-fs-on-usb-drive/"
slug = "raspberry-pi-root-fs-on-usb-drive"
tags = ["ARM","Kernel","Linux","Microcontroller","Raspberry Pi","USB"]
title = "Raspberry Pi Root FS on USB Drive"

+++

[![](http://mitchtech.net/wp-content/uploads/2012/06/pi-usb-drive-300x225.jpg)](http://mitchtech.net/raspberry-pi-audio/pi-usb-drive/)

This tutorial will demonstrate how to install the Debian root filestem (ie. '/') on a USB drive instead of the SD card. The SD card still retains the /boot partion and swap space. This requires a modified kernel to support the USB storage. You can [download the minimal modified kernel and modules here](http://dl.dropbox.com/u/1816557/bcmrpi_defconfig.tar)  or follow my [guide on how to compile it for yourself](http://mitchtech.net/raspberry-pi-kernel-compile/).

In either case, begin by installing the Debian image as you normally would to an SD card. Manually format the USB drive you intend to use as the root filesystem as ext4 using a utility like gparted.

Next, copy the root filesytem from the Debian install on the SD card to the USB drive, preserving attributes with the -a flag, substituting "sdcard-rootfs-partition-uuid" and "usbdrive-rootfs-partition-uuid" with the respective identifiers as the filesystem are mounted in Ubuntu.

```
sudo cp -a /media/sdcard-rootfs-partition-uuid/* /media/usbdrive-rootfs-partition-uuid/
sync
```

Now, delete the existing kernel.img and replace it with the new one, substituting "sdcard-boot-partition-uuid" with the identifier of the partion as it is mounted in Ubuntu.

```
sudo rm /media/sdcard-boot-partition-uuid/kernel.img
sudo mv kernel.img /media/sdcard-boot-partition-uuid/
```

Next, remove the existing /lib/modules and lib/firmware directories,

```
sudo rm -rf /media/usbdrive-rootfs-partition-uuid/lib/modules/
sudo rm -rf /media/usbdrive-rootfs-partition-uuid/lib/firmware/
```

and copy the new modules and firmware in their place:

```
cd ../../kernel/
sudo cp -a lib/modules/ /media/usbdrive-rootfs-partition-uuid/lib/
sudo cp -a lib/firmware/ /media/usbdrive-rootfs-partition-uuid/lib/
sync
```

Now we need to modify the location of the root partition in the /boot partion. This is contained within the file, cmdline.txt. In this file, change:

```
root=/dev/mmcblk0p2
```

to:

```
root=/dev/sda1
```

That's it! Plug in and boot up the root filesystem from the USB stick!

