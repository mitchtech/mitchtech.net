+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-06 00:15:42+00:00"
slug = "easy-gui-install-re-partition-raspberry-pi-on-ubuntu"
tags = ["GParted","Linux","Raspberry Pi","Ubuntu"]
title = "Easy GUI Install & Re-Partition Raspberry Pi on Ubuntu"
banner = "img/imagewriter.png"

+++

Easy Install & Resize the SD Card on the Raspberry Pi on Ubuntu.

First, open a terminal and install the ImageWriter and GParted utilities with apt-get

```
sudo apt-get install usb-imagewriter gparted
```

Assuming you are starting with a fresh install, download the newest release from the Raspberry Pi download site:

```
[http://www.raspberrypi.org/downloads](http://www.raspberrypi.org/downloads)
```

Extract the downloaded archive, and then open ImageWriter:

```
imagewriter
```

Select the desired .img file and target device, in this case, debian6-19-04-2012.img, and /dev/mmcblk0

![](/img/imagewriter.png)

Once the image write has completed, the next task is to repartition the SD card.  Note: this process can be done at any later as well, it is not limited to only during initial setup!  In any case, open a terminal, and start Gparted:

```
sudo gparted
```

The screen will display the current partition layout on the SD card, notably how much extra space is currently unused, in this case, almost 2GB.

![](/img/gparted-default.png)

The first step is to delete the swap partition at the bottom of the table  To do this, right click partition 3 (/dev/mmcblkp03) and select delete.  Notice that the operations pending section now displays this change.

Note: If the partitions are locked, they will need to first be unmounted before they can be modified.  To do so, right click on the partition, and select 'unmount' (Thanks Anand).

![](/img/gparted-delete-partition3.png)

Now, right click partition 2 (/dev/mmcblkp02) and select resize/move.  A pop-up will allow you to configure the partition:

![](/img/gparted-resize-pre.png)

Expand the partition, leaving free space at the end to be used for swap (512 MB below).  Make sure the 1 MB free space preceding doesn't change, and select None in the Align to box:

![](/img/gparted-resize-post.png)

Click the Resize/Move button, and you will return to the main screen.  Notice that the operations pending now also shows the grow operation.  Note:  If this displays move and grow, instead of just grow, cancel the operation and try again.

![](/img/gparted-resize-done.png)

Now we create the swap partition at the end. Right click on the remining unallocated space, and click new.  Expand the partition to fill the maximum available space, and set the file system type to linux-swap:

![](/img/gparted-new-swap.png)

Click add, and return again to the main screen, which now displays all three pending operations:

![](/img/gparted-everything-ready.png)

If everything looks good, click the checkmark in the header bar to apply the changes, and confirm the pop-up warnings.  Once finished, you will see the final result:

![](/img/gparted-everything-complete.png)

Close out of GParted, and eject the SD card.  It is already unmounted from the partitioning operation. Enjoy the extra space on your Raspberry Pi!

