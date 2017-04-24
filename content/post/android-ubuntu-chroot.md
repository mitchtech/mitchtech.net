+++
author = "michael"
categories = ["Android","Android Linux Chroot","Tutorials"]
comments = true
date = "2012-05-02 13:52:29+00:00"
slug = "android-ubuntu-chroot"
tags = ["Android","Chroot","Hack","Linux","Rootstock","Ubuntu","Virtual Machine"]
title = "Android + Ubuntu Chroot"

+++

Here is a quick overview of the process to create a Ubuntu system image that is bootable with Android chroot. It uses the rootstock utility to setup the initial image, including release version, username/password, image size, as well as to seed the desired packages to be pre-installed with the distro. For complete options with rootstock, consult the man pages.

Quickstart:

```
mkdir ubuntu

cd ubuntu

sudo rootstock \

--fqdn ubuntu \

--login ubuntu \

--password ubuntu \

--imagesize 4G \

--dist maverick \

--seed linux-image-omap,build-essential,mysql-server,tightvncserver,lxde,\

mysql-server-core-5.5,mysql-server-5.5,libmysqlclient16,mysql-common,\

mysql-client-core-5.5

dd if=/dev/zero of=ubuntu.img bs=1MB count=0 seek=4096

mke2fs -F ubuntu.img

mkdir ubuntumnt

sudo mount -o loop ubuntu.img ubuntumnt

sudo tar -C ubuntumnt -zxf armel-rootfs-XXXXXXXXXXXX.tgz

sudo umount ubuntumnt

sudo rm armel-rootfs-XXXXXXXXXXXX.tgz

sudo rm -rf ubuntumnt

cd ..

adb push ubuntu/ /sdcard/ubuntu
```

NOTE: XXXXXXXXXXXX is the timestamp for the file creation, for example: armel-rootfs-201203201350.tgz

Steps explained:

First, make a directory to store the ubuntu image and scripts

```
mkdir ubuntu

cd ubuntu
```

Next, execute rootstock as root. The options can be configured to create the image of your choosing. For example, if you wont be using a GUI in the chroot, you may want to omit the ‘lxde’ and ‘tightvncserver’ packages. You can also modify the image size if you desire as well, but remember that the maximum filesize on a FAT32 filesystem is 4GB (and your sdcard is very likely formatted as FAT32).

```
sudo rootstock \

--fqdn ubuntu \

--login ubuntu \

--password ubuntu \

--imagesize 4G \

--dist oneiric \

--seed linux-image-omap,build-essential,mysql-server,tightvncserver,lxde,\

mysql-server-core-5.5,mysql-server-5.5,libmysqlclient16,mysql-common,\

mysql-client-core-5.5
```

Now we need to create a blank filesystem image to extract the rootstock onto. For this task, we use the dd command. Remember to set the seek paramater to match the imagesize you created in the previous step.

```
dd if=/dev/zero of=ubuntu.img bs=1MB count=0 seek=4096
```

Use mke2fs to create a new filesystem on the created image file.

```
mke2fs -F ubuntu.img
```

Make a directory to serve as a mountpoint for the ubuntu image.

```
mkdir ubuntumnt
```

Next we need access to the filesystem we just created. This is accomplished by mounting the image file as a disk using the loopback device.

```
sudo mount -o loop ubuntu.img ubuntumnt
```

Now we use tar to extract the contents of the created ARM root filesystem to the image mounted on the loopback. Replace XXXXXXXXXXXX with the timestamp that was created with rootstock. E.g. armel-rootfs-201104151837.tgz

```
sudo tar -C ubuntumnt -zxf armel-rootfs-XXXXXXXXXXXX.tgz
```

Now that were finished with the extraction, we can unmount the system image.

```
sudo umount ubuntumnt
```

Were now finished with the desktop portion of the install, so can safely remove the tar of the image, and its mountpoint.

```
sudo rm armel-rootfs-XXXXXXXXXXXX.tgz

sudo rm -rf ubuntumnt
```

Switch to the parent directory, then use ADB to push the contents of the chroot install to the sdcard.

```
cd ..

adb push ubuntu/ /sdcard/ubuntu
```

Clone the scripts from my github repo:

```
git clone git://github.com/mitchtech/chroot_android.git -b ubuntu

cd chroot_android

tar -cvf ubuntu.tar *

./adb push ubuntu.tar /sdcard/ubuntu/
```

ADB shell into the device

```
./adb shell
```

Get root and change into the Ubuntu directory

```
su

cd /sdcard/ubuntu
```

Uncompress the image and scripts:

```
tar -xvf ubuntu.tar
```

Next run the installer script.

```
sh ./installubuntu.sh
```

Now, to start Ubuntu type ‘startubuntu’. Once Ubuntu started, to gain shell type ‘ubuntu’. To shutdown type ‘stopubuntu’.

```
startubuntu

ubuntu
```

If all goes well, you’ll be in the Ubuntu chroot:

If you get ‘root@localhost:/#’ then you know it’s working!
