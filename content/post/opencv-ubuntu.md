+++
author = "michael"
categories = ["Tutorials","Ubuntu"]
comments = true
date = "2012-05-02 15:52:18+00:00"
slug = "opencv-ubuntu"
tags = ["C","Computer Vision","Device Driver","Face Detection","Linux","Motion Tracking","OpenCV","OpenNI","PrimeSense","Ubuntu","Webcam"]
title = "OpenCV + Ubuntu"

+++

{{< youtube rIyGrhDYs0A >}}

Building OpenCV 2.3.1 from source on Ubuntu 12.04 x64. Here is an overview of the compilation of OpenCV with x264 and ffmpeg builtin. If you have completed my [Kinect + OpenNI + PrimeSense](http://mitchtech.net/ubuntukinect-openni-primesense/)tutorial, this will also support the OpenNI and PrimeSense drivers with OpenCV. This is largely based on the wonderful OpenCV tutorials from [Sebastian Montabone](http://www.samontab.com/web/2011/06/installing-opencv-2-2-in-ubuntu-11-04/) and [Osman Eralp](http://www.ozbotz.org/opencv-installation/). Before you start, make sure to have removed ffmpeg and x264 (if applicable):

```
sudo apt-get remove ffmpeg x264 libx264-dev
```

Now begin by installing the required dependencies:

```
sudo apt-get install build-essential libgtk2.0-0 libgtk2.0-dev gtk2-engines-pixbuf libjpeg-dev libtiff4-dev libjasper-dev libopenexr-dev cmake cmake-qt-gui python-dev python-numpy python-sphinx libtbb-dev libeigen2-dev yasm libmp3lame-dev libfaac-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev libhighgui-dev libgtkglext1-dev libdc1394-22-dev libboost-all-dev qtcreator libwxbase2.8-dev libwxgtk2.8-dev wx-common checkinstall libjack-jackd2-dev libsdl1.2-dev libva-dev libvdpau-dev libx11-dev libxfixes-dev texi2html zlib1g-dev libgstreamer0.10-0 libgstreamer0.10-dev gstreamer0.10-tools gstreamer0.10-plugins-base libgstreamer-plugins-base0.10-dev gstreamer0.10-plugins-good gstreamer0.10-plugins-ugly gstreamer0.10-plugins-bad gstreamer0.10-ffmpeg libv4l-dev
```

Create a directory for the sources:

```
mkdir ~/opencv cd ~/opencv
```

Next, clone, build and install x264:

```
git clone git://git.videolan.org/x264.git

cd x264

./configure --enable-static --enable-pic --enable-shared

make

sudo make install
```

The next step is to build and install ffmpeg:

```
cd ~/opencv

wget http://ffmpeg.org/releases/ffmpeg-0.8.10.tar.bz2

tar -xvjpf ffmpeg-0.8.10.tar.bz2

cd ffmpeg-0.8.10/

./configure --enable-gpl --enable-version3 --enable-nonfree --enable-postproc --enable-libfaac --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libtheora --enable-libvorbis --enable-libmp3lame --enable-libx264 --enable-libxvid --enable-x11grab --enable-swscale --enable-pic --enable-shared

make

sudo make install
```

NOTE: Do NOT clone the mainline source tree with git. This version is NOT compatible (I tried and failed several times!). I’m sure version 0.7 and 0.8 work, anything newer resulted in compilation errors later in the OpenCV build. Next, build and install OpenCV:

```
cd ~/opencv

wget http://downloads.sourceforge.net/project/opencvlibrary/opencv-unix/2.3.1/OpenCV-2.3.1a.tar.bz2

tar -xvjpf OpenCV-2.3.1a.tar.bz2

cd OpenCV-2.3.1/

mkdir build

cd build

cmake-gui ..
```

Now click ‘configure’ and check the following boxes:

```
BUILD_EXAMPLES

INSTALL_C_EXAMPLES

INSTALL_PYTHON_EXAMPLES

WITH_OPENNI

WITH_TBB
```

NOTE: you can also enable the CUDA extensisons if you have capable nvidia graphics card(s). Click ‘configure’ again, check the output and ensure that there are not any modules that cmake cannot find. If everything looks good, click ‘generate’ to create the makefiles, then close cmake-gui.

```
make

sudo make install
```

Finally, we need to make a few configurations for OpenCV. First, open the opencv.conf file with the following code:

```
sudo gedit /etc/ld.so.conf.d/opencv.conf
```

Add the following line at the end of the file(it may be an empty file, that is ok) and then save it:

```
/usr/local/lib
```

Then edit the system-wide bashrc file:

```
sudo gedit /etc/bash.bashrc
```

Add the following new lines to the end of the file:

```
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig export PKG_CONFIG_PATH
```

Now that everything is installed and configured, on to the demos!

```
cd ~/opencv/OpenCV-2.3.1/build/bin
```

Build/bin demos worth checking out that don’t require a webcam:

{{< youtube Y35oHgitZsY >}}

```
convexhull

kmeans

drawing
```

Build/bin demos using camera:

{{< youtube ena9Sw6CwhY >}}

```
adaptiveskindetector

facedetect

fback

bgfg_segm c true

lkdemo

motempl
```

