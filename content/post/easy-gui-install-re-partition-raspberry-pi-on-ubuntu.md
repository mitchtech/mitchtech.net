+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-06 00:15:42+00:00"
layout = "post"
link = "http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/"
slug = "easy-gui-install-re-partition-raspberry-pi-on-ubuntu"
tags = ["GParted","Linux","Raspberry Pi","Ubuntu"]
title = "Easy GUI Install & Re-Partition Raspberry Pi on Ubuntu"

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

[![](http://mitchtech.net/wp-content/uploads/2012/06/imagewriter-300x146.png)](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/imagewriter/)

Once the image write has completed, the next task is to repartition the SD card.  Note: this process can be done at any later as well, it is not limited to only during initial setup!  In any case, open a terminal, and start Gparted:

```
sudo gparted
```

The screen will display the current partition layout on the SD card, notably how much extra space is currently unused, in this case, almost 2GB.

[![](http://mitchtech.net/wp-content/uploads/2012/06/gparted-default-300x204.png)](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/gparted-default/)

The first step is to delete the swap partition at the bottom of the table  To do this, right click partition 3 (/dev/mmcblkp03) and select delete.  Notice that the operations pending section now displays this change.

Note: If the partitions are locked, they will need to first be unmounted before they can be modified.  To do so, right click on the partition, and select 'unmount' (Thanks Anand).

[![](http://mitchtech.net/wp-content/uploads/2012/06/gparted-delete-partition3-300x204.png)](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/gparted-delete-partition3/)

Now, right click partition 2 (/dev/mmcblkp02) and select resize/move.  A pop-up will allow you to configure the partition:

[![](http://mitchtech.net/wp-content/uploads/2012/06/gparted-resize-pre-300x160.png)](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/gparted-resize-pre/)

Expand the partition, leaving free space at the end to be used for swap (512 MB below).  Make sure the 1 MB free space preceding doesn't change, and select None in the Align to box:

[![](http://mitchtech.net/wp-content/uploads/2012/06/gparted-resize-post-300x160.png)](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/gparted-resize-post/)

Click the Resize/Move button, and you will return to the main screen.  Notice that the operations pending now also shows the grow operation.  Note:  If this displays move and grow, instead of just grow, cancel the operation and try again.

[![](http://mitchtech.net/wp-content/uploads/2012/06/gparted-resize-done-300x204.png)](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/gparted-resize-done/)

Now we create the swap partition at the end. Right click on the remining unallocated space, and click new.  Expand the partition to fill the maximum available space, and set the file system type to linux-swap:

[![](http://mitchtech.net/wp-content/uploads/2012/06/gparted-new-swap-300x150.png)](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/gparted-new-swap/)

Click add, and return again to the main screen, which now displays all three pending operations:

[![](http://mitchtech.net/wp-content/uploads/2012/06/gparted-everything-ready-300x204.png)](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/gparted-everything-ready/)

If everything looks good, click the checkmark in the header bar to apply the changes, and confirm the pop-up warnings.  Once finished, you will see the final result:

[![](http://mitchtech.net/wp-content/uploads/2012/06/gparted-everything-complete-300x204.png)](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/gparted-everything-complete/)

Close out of GParted, and eject the SD card.  It is already unmounted from the partitioning operation. Enjoy the extra space on your Raspberry Pi!

