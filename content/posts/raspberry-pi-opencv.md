+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-14 23:41:41+00:00"
excerpt = "OpenCV is a suite of powerful computer vision tools. Here is a quick overview of how I installed OpenCV on my Raspberry Pi with debian6-19-04-2012."
slug = "raspberry-pi-opencv"
tags = ["ARM","C","Computer Vision","Face Detection","Linux","Motion Tracking","OpenCV","Python","Raspberry Pi","Webcam"]
title = "Raspberry Pi + OpenCV"
banner = "https://img.youtube.com/vi/9zgVG_gWeVc/0.jpg"

+++

{{< youtube 9zgVG_gWeVc >}}

OpenCV is a suite of powerful computer vision tools. Here is a quick overview of how I installed OpenCV on my Raspberry Pi with [debian6-19-04-2012.](http://downloads.raspberrypi.org/images/debian/6/debian6-19-04-2012/debian6-19-04-2012.zip)  The guide is based on the official [OpenCV Installation Guide on Debian and Ubuntu](http://opencv.willowgarage.com/wiki/InstallGuide%20%3A%20Debian). Before you begin, make sure you have expanded your SD card to allow for the install of OpenCV. Its a big package with lots of dependencies. You can follow my instructions [here](http://mitchtech.net/easy-gui-install-re-partition-raspberry-pi-on-ubuntu/).  Once you have expanded the SD card, open up a terminal and install the following packages:

**UPDATE:** You can execute the following steps with a simple call to the Ansible playbook [playbook-opencv](http://goo.gl/INfRQI). Note that you have to edit the `pis.yml` file with your pi ip address and update `group_vars/pis.yml` with your pi password.

```
git clone https://github.com/chrismeyersfsu/playbook-opencv.git
ansible-playbook site.yml -i pis.yml -vvvv
```

**Note:** The make command will take HOURS to run. Please be patient.

```
sudo apt-get -y install build-essential cmake cmake-qt-gui pkg-config libpng12-0 libpng12-dev libpng++-dev libpng3 libpnglite-dev zlib1g-dbg zlib1g zlib1g-dev pngtools libtiff4-dev libtiff4 libtiffxx0c2 libtiff-tools
sudo apt-get -y install libjpeg8 libjpeg8-dev libjpeg8-dbg libjpeg-progs ffmpeg libavcodec-dev libavcodec53 libavformat53 libavformat-dev libgstreamer0.10-0-dbg libgstreamer0.10-0 libgstreamer0.10-dev libxine1-ffmpeg libxine-dev libxine1-bin libunicap2 libunicap2-dev libdc1394-22-dev libdc1394-22 libdc1394-utils swig libv4l-0 libv4l-dev python-numpy libpython2.6 python-dev python2.6-dev libgtk2.0-dev pkg-config
```

There are some dependency issues with the order of the install, mostly with regard to libjpeg issues, so be sure to install in this order. You will see some broken package errors if you attempt to install all the dependencies in one step.

Next, pull down the source files for OpenCV using wget:

```
wget http://sourceforge.net/projects/opencvlibrary/files/opencv-unix/2.3.1/OpenCV-2.3.1a.tar.bz2
```

Once finished downloading, extract the archive, remove the no longer needed archive (to save space), change directory to the top of the source tree, make a directory for the build, and change into it:

```
tar -xvjpf OpenCV-2.3.1a.tar.bz2
rm OpenCV-2.3.1a.tar.bz2
cd OpenCV-2.3.1/
mkdir build
cd build
```

Next, you will need to configure the build using cmake. If you aren't sure about what options you want/need or are unfamiliar with cmake, this line will create a standard configuration:

```
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_PYTHON_SUPPORT=ON -D BUILD_EXAMPLES=ON ..
```

Alternatively, you can configure the build using a GUI interface. This can be helpful to build with support for additional OpenCV features. To use the cmake GUI, run:

```
cmake-gui ..
```

In the cmake GUI, click ‘configure’ to pre-populate the build options. Select or remove any desired features, then click ‘configure’ again, check the output and ensure that there are not any modules that cmake cannot find. If everything looks good, click ‘generate’ to create the makefiles, then close cmake-gui. Now we are ready to start the build! To compile, run make, then install with make install:

```
make
sudo make install
```

This will take a LONG time... over four and a half hours to compile natively!

Finally, we need to make a few configurations for OpenCV. First, open the opencv.conf file with the following code:

```
sudo nano /etc/ld.so.conf.d/opencv.conf
```

Add the following line at the end of the file(it may be an empty file, that is ok) and then save it:

```
/usr/local/lib
```

Then edit the system-wide bashrc file:

```
sudo nano /etc/bash.bashrc
```

Add the following new lines to the end of the file:

```
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig export PKG_CONFIG_PATH
```

Now that everything is installed and configured, on to the demos!  The C demos are here:

```
cd ~/opencv/OpenCV-2.3.1/build/bin
```

C demos in build/bin demos worth checking out (that don’t require a webcam):

```
convexhull

kmeans

drawing
```

The python demos are located in samples/python:

```
cd ~/opencv/OpenCV-2.3.1/build/bin
```

These demos also don't require a webcam:

```
python ./minarea.py

python ./delaunay.py

python ./drawing.py
```

