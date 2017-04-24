+++
author = "meyers"
categories = ["Beaglebone","Tutorials"]
comments = true
date = "2013-06-30 18:15:51+00:00"
layout = "post"
link = "http://mitchtech.net/beaglebone-ubuntu/"
slug = "beaglebone-ubuntu"
title = "Beaglebone + Ubuntu"

+++

We can install Ubuntu 2-ways:

  1. To the external SDCARD
  2. To the internal MMC

Installing to the internal MMC requires an SDCARD to install, but the sdcard is not required after that. The process is mostly the same. The MMC setup vs. the SDCARD setup depends on which image you download.

## Installing Ubuntu

  * **MMC:** [Download](http://rcn-ee.net/deb/flasher/raring/) the latest file of the form _BBB-eMMC-flasher-ubuntu-xx.xx-xxxx-xx-xx.img.xz_

  * **SDCARD:** [Download](http://rcn-ee.net/deb/rootfs/quantal/) the latest file of the form _ubuntu-12.10-console-armhf-xxxx-xx-xx.tar.xz_

Extract the image

```
sudo apt-get install xz
xz -d *.img.xz
```

Insert the sdcard into your desktop and note the device path. In my case the device is at _/dev/sdc_.

```
meyers@mcbeefy:~/beaglebone$ dmesg
[ 1659.900631] usb 3-1: USB disconnect, device number 3
[ 2664.433700] usb 3-1: new high-speed USB device number 4 using xhci_hcd
[ 2664.709199] scsi7 : usb-storage 3-1:1.0
[ 2665.706903] scsi 7:0:0:0: Direct-Access Generic- SD/MMC 1.00 PQ: 0 ANSI: 0 CCS
[ 2665.707747] sd 7:0:0:0: Attached scsi generic sg3 type 0
[ 2666.334388] sd 7:0:0:0: [sdc] 15519744 512-byte logical blocks: (7.94 GB/7.40 GiB)
[ 2666.334770] sd 7:0:0:0: [sdc] Write Protect is off
[ 2666.334775] sd 7:0:0:0: [sdc] Mode Sense: 03 00 00 00
[ 2666.335066] sd 7:0:0:0: [sdc] No Caching mode page present
[ 2666.335071] sd 7:0:0:0: [sdc] Assuming drive cache: write through
[ 2666.336660] sd 7:0:0:0: [sdc] No Caching mode page present
[ 2666.336667] sd 7:0:0:0: [sdc] Assuming drive cache: write through
[ 2666.337339] sdc: sdc1 sdc2
[ 2666.338721] sd 7:0:0:0: [sdc] No Caching mode page present
[ 2666.338726] sd 7:0:0:0: [sdc] Assuming drive cache: write through
[ 2666.338730] sd 7:0:0:0: [sdc] Attached SCSI removable disk
[ 2666.821868] EXT4-fs (sdc2): mounted filesystem with ordered data mode. Opts: (null)
```

Flash the image to the sdcard. Substitute _<mmc_or_sdcard>.img_ and _/dev/sdX_ accordingly.

```
sudo dd if=<mmc_or_sdcard>.img of=/dev/sdX bs=1M

```

Upon completion remove the sdcard and perform the following:

  * Ensure the beaglebone is off

  * If you plan on powering the beaglebone with usb, ensure the ethernet is unplugged.

  * Insert the sdcard into the beaglebone

  * Hold down the button that is by itself near the SDCARD

  * Insert the USB power or barrel jack power

  * Once the lights begin blinking blue you may release the button

  * Wait =~ 45 minutes until all the lights are blue 

Once all the lights turn solid blue the MMC is successfully flashed and you may power down your beaglebone (unplug the power), remove the sdcard. Wait a couple seconds, then plug the power back in and the system will boot Ubuntu.

### Verifying Ubuntu Install

Find the ip of your beaglebone on your network.

```
meyers@mcbeefy:~$ sudo nmap -sP 192.168.1.*
Starting Nmap 5.21 ( http://nmap.org ) at 2013-06-30 14:13 EDT
Nmap scan report for 192.168.1.1
Host is up (0.00086s latency).
MAC Address: 00:23:69:0E:20:D7 (Cisco-Linksys)
Nmap scan report for 192.168.1.2
Host is up (0.076s latency).
MAC Address: BC:AE:C5:C4:F6:AB (Unknown)
Nmap scan report for 192.168.1.103
Host is up (0.065s latency).
MAC Address: BC:AE:C5:C4:F6:AB (Unknown)
Nmap scan report for 192.168.1.106
Host is up (0.00023s latency).
MAC Address: 3C:07:71:24:21:4B (Unknown)
Nmap scan report for 192.168.1.107
Host is up.
Nmap scan report for 192.168.1.112
Host is up (0.075s latency).
MAC Address: BC:AE:C5:C4:F6:AB (Unknown)
Nmap scan report for 192.168.1.114
Host is up (0.062s latency).
MAC Address: BC:AE:C5:C4:F6:AB (Unknown)
Nmap scan report for 192.168.1.116
Host is up (0.00072s latency).
MAC Address: C8:A0:30:B2:8E:5D (Unknown)
Nmap scan report for 192.168.1.118
Host is up (0.017s latency).
MAC Address: BC:AE:C5:C4:F6:AB (Unknown)
Nmap done: 256 IP addresses (9 hosts up) scanned in 6.18 seconds
```

ssh to your beaglebone.

```
ssh ubuntu@192.168.1.116
ubuntu@192.168.1.116's password: temppwd
```
