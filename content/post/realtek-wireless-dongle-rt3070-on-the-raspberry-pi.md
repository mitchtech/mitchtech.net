+++
author = "meyers"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-03 18:49:22+00:00"
slug = "realtek-wireless-dongle-rt3070-on-the-raspberry-pi"
tags = ["ARM","Device Driver","Linux","Raspberry Pi","realtek","rt2661","rt2860","rt2870","rt3070","rt3071","rt3090"]
title = "Ralink/Realtek Wireless Dongle (rt3070) on the Raspberry Pi"
banner = "img/raspi-realtek.jpg"

+++

![](/img/raspi-realtek.jpg)

## Scenario

You have a HAWKING HWUN3 Hi-Gain Wireless Adapter dongle that you want to use on your Raspberry Pi running debian.

Note: the same set of steps will probably work for other variations of Ralink/Realtek wifi dongles [rt2561,rt2661,rt2860,rt2870,rt3070,rt3071,rt3090].

## The Problem

The standard release (debian6-19-04-2012.zip) contains the needed drivers however, the firmware needed is not included. The following tutorial will describe how to get and "install" the needed firmware.
You will notice the firmware problem if after plugging in your wifi dongle you type dmesg and it complains about not being able to find the firmware.

```
dmesg
usb 1-1.2: USB disconnect, device number 4
usb 1-1.2: new high speed USB device number 6 using dwc_otg
usb 1-1.2: New USB device found, idVendor=0e66, idProduct=0013
usb 1-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 1-1.2: Product: 802.11 n WLAN
usb 1-1.2: Manufacturer: Ralink
usb 1-1.2: SerialNumber: 1.0
cfg80211: Calling CRDA to update world regulatory domain
usb 1-1.2: reset high speed USB device number 6 using dwc_otg
ieee80211 phy0: Selected rate control algorithm 'minstrel_ht'
Registered led device: rt2800usb-phy0::radio
Registered led device: rt2800usb-phy0::assoc
Registered led device: rt2800usb-phy0::quality
usbcore: registered new interface driver rt2800usb
phy0 -> rt2x00lib_request_firmware: Error - Failed to request Firmware.
phy0 -> rt2x00lib_request_firmware: Error - Failed to request Firmware.
phy0 -> rt2x00lib_request_firmware: Error - Failed to request Firmware.
phy0 -> rt2x00lib_request_firmware: Error - Failed to request Firmware.
```

## The Solution

To fix the described problem we need to make the firmware available to the system by placing it in /lib/firmware/. How do you know if the solution provided works or not? The kernel will continually complain about not being able to find the firmware. Then, when the firmware is found, the kernel will stop complaining. You can monitor the complaints with the tail command.

Execute lsusb after you have inserted the wireless usb dongle to get more information about your device.

```
lsusb
Bus 001 Device 006: ID 0e66:0013 Hawking Technologies HWUN3 Hi-Gain Wireless-N Adapter [Ralink RT3070]
Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp.
Bus 001 Device 005: ID 413c:2003 Dell Computer Corp. Keyboard
Bus 001 Device 002: ID 0424:9512 Standard Microsystems Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

Ensure that the kernel you are running has loaded the required modules.

```
lsmod
Module Size Used by
arc4 764 2
rt2800usb 9148 0
rt2800lib 37652 1 rt2800usb
crc_ccitt 932 1 rt2800lib
rt2x00usb 6532 1 rt2800usb
rt2x00lib 25780 3 rt2800usb,rt2800lib,rt2x00usb
mac80211 171628 3 rt2800lib,rt2x00usb,rt2x00lib
cfg80211 123084 2 rt2x00lib,mac80211
fuse 49036 1
evdev 6404 1
joydev 7576 0
```

Monitoring the status of the firmware fix.

```
tail -f /var/log/syslog
```

Acquiring and installing the firmware.

```
sudo apt-get install git-core
git clone http://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
cp linux-firmware/rt2870.bin /lib/firmware/rt2870.bin
```
