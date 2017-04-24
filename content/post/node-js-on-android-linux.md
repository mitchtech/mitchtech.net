+++
author = "michael"
categories = ["Android","Android Linux Chroot","Tutorials"]
comments = true
date = "2012-05-02 13:53:58+00:00"
layout = "post"
link = "http://mitchtech.net/node-js-on-android-linux/"
slug = "node-js-on-android-linux"
tags = ["Android","Chroot","Hack","Linux","Node.js","Rootstock","Ubuntu","Virtual Machine"]
title = "Android + Linux Chroot + Node.js"

+++

This article will walk you through how to compile, from source, node.js on Android.  After installing node.js on about 4 different devices (Thunderbolt, Incredible, two G1’s, Galaxy S) I decided to compile this tutorial.

## Prerequisites

  * Android running Debian in a chroot(ed) environment.

  * Environment contains the necessary path(s)

```
vim /etc/bashrc
PATH=$PATH:/usr/local/bin
```

#### Swap File (G1 only?)

The RAM in both the Incredible and Thunderbolt are sufficient to compile node.js.  The G1 however, requires a swap file to supplement the small amount of RAM to successfully compile node.js.  The gcc compilation failed when I tried a swap fall as small as 64 MB.  512MB swap file was used for a successful compilation.

```
524388 MB swap file
dd if=/dev/zero of=/swapfile1 bs=1024 count=524388
```

```
mkswap /swapfile1
chmod 0600 /swapfile1
swapon /swapfile1
```

```
vim /etc/fstab
/swapfile1 swap swap defaults 0 0
```

## Node.js and Dependencies

  1. Download dependencies

  2. Download the node.js source and checkout a version known to work

  3. Patch, configure, and make

```
apt-get install git-core
apt-get install python g++ libssl-dev make pkg-config
./configure
make
make install
```

```
git clone https://github.com/joyent/node.git
cd node
git checkout v0.6.8
```

To patch node.js source create a file in the node root directory called patch and paste one of the following diff’s.  Next, run patch < patch.

#### G1 Patch

```
diff –git a/deps/v8/SConstruct b/deps/v8/SConstruct
index 1dcdce4..a5aaf50 100644
— a/deps/v8/SConstruct
+++ b/deps/v8/SConstruct
@@ -79,7 +79,7 @@ LIBRARY_FLAGS = {
},
‘gcc’: {
‘all’: {
-      ’CCFLAGS’:      ['$DIALECTFLAGS', '$WARNINGFLAGS'],
+      ’CCFLAGS’:      ['$DIALECTFLAGS', '$WARNINGFLAGS','-march=armv5t','-mno-thumb-interwork'],
‘CXXFLAGS’:     ['-fno-rtti', '-fno-exceptions'],
},
‘visibility:hidden’: {
@@ -154,12 +154,12 @@ LIBRARY_FLAGS = {
},
‘armeabi:softfp’ : {
‘CPPDEFINES’ : ['USE_EABI_HARDFLOAT=0'],
-        ’vfp3:on’: {
-          ’CPPDEFINES’ : ['CAN_USE_VFP_INSTRUCTIONS']
-        },
-        ’simulator:none’: {
-          ’CCFLAGS’:     ['-mfloat-abi=softfp'],
-        }
+#        ’vfp3:on’: {
+#          ’CPPDEFINES’ : ['CAN_USE_VFP_INSTRUCTIONS']
+#        },
+#        ’simulator:none’: {
+#          ’CCFLAGS’:     ['-mfloat-abi=softfp'],
+#        }
},
‘armeabi:hard’ : {
‘CPPDEFINES’ : ['USE_EABI_HARDFLOAT=1'],
```

#### Galaxy S Patch

```
diff –git a/deps/v8/SConstruct b/deps/v8/SConstruct
index 1dcdce4..a5aaf50 100644
— a/deps/v8/SConstruct
+++ b/deps/v8/SConstruct
@@ -79,7 +79,7 @@ LIBRARY_FLAGS = {
},
‘gcc’: {
‘all’: {
-      ’CCFLAGS’:      ['$DIALECTFLAGS', '$WARNINGFLAGS'],
+      ’CCFLAGS’:      ['$DIALECTFLAGS', '$WARNINGFLAGS','-march=armv5t'],
‘CXXFLAGS’:     ['-fno-rtti', '-fno-exceptions'],
},
‘visibility:hidden’: {
@@ -154,12 +154,12 @@ LIBRARY_FLAGS = {
},
‘armeabi:softfp’ : {
‘CPPDEFINES’ : ['USE_EABI_HARDFLOAT=0'],
-        ’vfp3:on’: {
-          ’CPPDEFINES’ : ['CAN_USE_VFP_INSTRUCTIONS']
-        },
-        ’simulator:none’: {
-          ’CCFLAGS’:     ['-mfloat-abi=softfp'],
-        }
+#        ’vfp3:on’: {
+#          ’CPPDEFINES’ : ['CAN_USE_VFP_INSTRUCTIONS']
+#        },
+#        ’simulator:none’: {
+#          ’CCFLAGS’:     ['-mfloat-abi=softfp'],
+#        }
},
‘armeabi:hard’ : {
‘CPPDEFINES’ : ['USE_EABI_HARDFLOAT=1'],
```

## Node.js Libraries

Installing the below libraries are optional. This section is included for users that wish to setup node.js to control an arduino powered laser turret.

```
npm install express
npm install socket.io
npm install jquery
```
