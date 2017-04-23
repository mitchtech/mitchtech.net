---
author: michael
comments: true
date: 2012-05-16 23:39:35+00:00
layout: post
link: http://mitchtech.net/compile-cyanogenmod-9-for-galaxy-nexus/
slug: compile-cyanogenmod-9-for-galaxy-nexus
title: 'Compile Cyanogenmod 9 for Galaxy Nexus '
categories:
- Android
- Tutorials
- Ubuntu
tags:
- Android
- Kernel
- Linux
- Ubuntu
---

This tutorial will outline the process to compile Cyanogenmod 9 for the Verizon (LTE) Galaxy Nexus (aka toro, a variant of the tuna) on Ubuntu 12.04 LTS.  This process has changed a bit over time, notably with new hassles to configure the Oracle Java JDK.  While the tutorial is specific to the Galaxy Nexus, it generalizes to most devices supported by Cyanogenmod 9.  First, install and configure the Android SDK (more thorough info [here](http://developer.android.com/sdk/installing.html)):

```
wget http://dl.google.com/android/android-sdk_r18-linux.tgz

tar -xvzf android-sdk_r18-linux.tgz

rm android-sdk_r18-linux.tgz

cd android-sdk-linux

tools/android update sdk - -no-ui
```

It could take a while for the updates to the Android SDK to download and install. Once that has completed, install the package dependencies.

```
sudo apt-get install git-core gnupg flex bison gperf libsdl1.2-dev libesd0-dev libwxgtk2.6-dev squashfs-tools build-essential zip curl libncurses5-dev zlib1g-dev pngcrush schedtool lib32readline-gplv2-dev
```

The next step is to download and configure the most recent Java JDK from Oracle.  This part of the tutorial is based on a nice tutorial from [John Bokma](http://johnbokma.com/mexit/2011/06/24/oracle-java-jdk-installation-ubuntu.html).

```
Download the JDK from Oracle [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk-6u31-download-1501634.html):

sudo mkdir -p /usr/local/java

sudo mv ~/Downloads/jdk-6u31-linux-x64.bin /usr/local/java

cd /usr/local/java

sudo chmod +x jdk-6u31-linux-x64.bin

sudo ./jdk-6u31-linux-x64.bin
```

The installer will attempt to open a browser, but will fail. Presumably this is because the browser is unable to start as root, but this doesn't seem to affect the install at all.  Now remove the installer, and create a symlink to /usr/local/java/latest.  This way a new JDK can easily be configured by just moving the /usr/local/java/latest symlink to the most recent version:

```
sudo rm jdk-6u31-linux-x64.bin

sudo ln -s jdk1.6.0_31 /usr/local/java/latest
```

Next we will need to configure some environmental variables so the JDK will be recognized. Add the JAVA_HOME and JRE_HOME . For example,

```
sudo gedit /etc/environment
```

Then replace the contents with the following:

```
`JAVA_HOME="/usr/local/java/latest"` `JRE_HOME="/usr/local/java/latest/jre"` `PATH="/usr/local/java/latest/bin:\` `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games"
````

If you don't want to log out and log back in to have the updated /etc/environment parsed by the system, you can use the 'source' command:

```
source /etc/environment
```

You can test if it is working correctly using

```
java -version  #  and  javac -version
```

The output should look something like this:

```
java version "1.6.0_31" Java(TM) SE Runtime Environment (build 1.6.0_31-b04) Java HotSpot(TM) 64-Bit Server VM (build 20.6-b01, mixed mode)
```

Then, get the repo tool (a wrapper for git) and make it executable.

```
mkdir -p ~/bin
mkdir -p ~/cm

curl https://dl-ssl.google.com/dl/googlesource/git-repo/repo > ~/bin/repo

chmod a+x ~/bin/repo
```

Initialize and sync the repo. Change the -b option to checkout another branch (like -b gingerbread). NOTE: reboot may be required for repo to work!

```
cd ~/cm

repo init -u git://github.com/CyanogenMod/android.git -b ics

repo sync -j16
```

After the source has synched, we need to run a script to get the prebuilt binaries, including ROM Manager and Terminal.

```
cd ~/cm/vendor/cm

./get-prebuilts
```

Now setup the environment with envsetup

```
cd ~/cm

. build/envsetup.sh
```

Execute the 'brunch' command to see the list of build targets, and make your selection.  For the Galaxy Nexus, select cm_toro-userdebug, for Nexus S, select cm_crespo-userdebug, for Xoom, choose cm_wingray-userdebug

```
brunch
```

Once a selection is made, the build should start. If it doesn't, try running the 'lunch' instead. Make your selection, then run 'mka bacon'

```
lunch

mka bacon
```

If that doesn’t work either, explicitly execute 'make bacon'. You can use the -j compiler flag to enable parallel make.  The recommended use is 'processor cores + 1', e.g. 5 if you have a quad core processor:

```
make -j[#ofcpus] bacon
```

Once the build completes, the output will be located in ~/cm/out/target/product/toro/.  This folder contains the system and boot images, as well as a compressed and signed update.zip. Push the file to the sdcard of the device, and reboot into recovery:

```
adb push ~/cm/out/target/product/toro/update-cm-9.0.0-RC0-toro-UNOFFICIAL-signed.zip /sdcard/

adb reboot recovery
```

Once booted into recovery, MAKE A BACKUP, then flash the update.zip.

