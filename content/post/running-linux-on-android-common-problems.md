+++
author = "michael"
categories = ["Android","Android Linux Chroot","Tutorials"]
comments = true
date = "2012-05-02 13:55:10+00:00"
layout = "post"
link = "http://mitchtech.net/running-linux-on-android-common-problems/"
slug = "running-linux-on-android-common-problems"
tags = ["Android","Chroot","Hack","Linux","Node.js","Rootstock","Ubuntu","Virtual Machine"]
title = "Android + Linux Chroot + Common Problems"

+++

## Corrupted Filesystem

**_Problem: _**ext2 Distribution Image
**_Explanation: _**If you formated the distribution partition as ext2 then chances are you will have a filesystem corruption. The trouble is fsck doesn’t come with busybox and it’s hard to run fsck on your root filesytem while mounted. The solution is to mount the distribution image from another linux machine and run fsck.
**_Solution:_**

```
Disable USB debugging on your phone.
Plug your phone into a linux box.
Enable USB storage.
losetup /dev/loop0 /media//debian/debian.img
losetup /dev/loop0 /media//ubuntu/ubuntu.img
fsck /dev/loop0
losetup -d /dev/loop0
Eject the phone
```

## OpenSSH Server

_**Problem:**_ After installing openssh-server bash ./bootdebian or ./bootubuntu console displays I have no name!@localhost:/etc#
_**Explanation:**_ openssh-server crashed in the middle of installing. Part of the installation process involves moving /etc/passwd to /etc/passwd-.
_**Solution:**_ The device might reboot after running dpkg.

```
mv /etc/passwd- /etc/passwd
mv /etc/shadow- /etc/shadow
dpkg –configure -a
```

_**Problem:**_ Starting sshd reboots phone (G1)
_**Explanation:**_ Android doesn’t like ipv6
_**Solution:**_ Add the below line to both /etc/ssh/ssh_config and /etc/ssh/sshd_config

```
AddressFamily inet
```

_**Problem:**_ PTY allocation request failed on channel 0
_**Explanation:**_ sshd reports:

```
openpty: No such file or directory
session_pty_req: session 0 alloc failed
```

_**Solution:**_

```
/sbin/MAKEDEV pts
mount /dev/pts
```

_**Problem:**_ sshing to the phone simply hangs (G1)
_**Explanation:**_ Something to do with if proc doesn’t exist then selinux is used and selinux doesn’t really exist on android.
_**Solution:**_ Add the below line to /root/.bashrc

```
mount -t proc proc /proc
```

_**Alternative Solution:**_ Add the below line to /root/.bashrc

```
none /proc proc defaults
```

