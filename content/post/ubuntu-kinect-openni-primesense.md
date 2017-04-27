+++
author = "michael"
categories = ["Kinect","Tutorials","Ubuntu"]
comments = true
date = "2012-05-02 05:15:31+00:00"
slug = "ubuntu-kinect-openni-primesense"
tags = ["Hack","Kinect","Linux","OpenNI","PrimeSense","Ubuntu"]
title = "Ubuntu + Kinect + OpenNI + PrimeSense"

+++

{{< youtube BL_EPfP7T50 >}}

#### Getting the OpenNI and PrimeSense drivers working on Ubuntu

Here’s an overview of the process to get the OpenNI and PrimeSense drivers working with the Kinect and Ubuntu. Begin by installing some dependencies:

```
sudo apt-get install git-core cmake freeglut3-dev pkg-config build-essential libxmu-dev libxi-dev libusb-1.0-0-dev doxygen graphviz mono-complete
```

Make a directory to store the build, then clone the OpenNI source from Github.

```
mkdir ~/kinect
cd ~/kinect
git clone https://github.com/OpenNI/OpenNI.git
```

Run the RedistMaker script in the Platform/Linux folder and install the output binaries

```
cd OpenNI/Platform/Linux/CreateRedist/
chmod +x RedistMaker
./RedistMaker
cd ../Redist/OpenNI-Bin-Dev-Linux-x64-v1.5.2.23/
sudo ./install.sh
```

Next, clone the Avin2 SensorKinect source from Github.

```
cd ~/kinect/
git clone git://github.com/avin2/SensorKinect.git
```

Run the RedistMaker script in the Platform/Linux folder and install the output binaries.

```
cd SensorKinect/Platform/Linux/CreateRedist/
chmod +x RedistMaker
./RedistMaker
cd ../Redist/Sensor-Bin-Linux-x64-v5.1.0.25/
chmod +x install.sh
sudo ./install.sh
```

Then download the [OpenNI Compliant Middleware Binaries](http://www.openni.org/Downloads/OpenNIModules.aspx) to ~/kinect
Select these options from the dropdown menus:
Unstable
PrimeSense NITE Unstable Build for Ubuntu 10.10 x64 v 1.5.2.21

Extract the contents of the archive and switch to the Data directory contained within.

```
cd ~/kinect
tar -xvjpf nite-bin-linux-x64-v1.5.2.21.tar.bz2
cd NITE-Bin-Dev-Linux-x64-v1.5.2.21/Data
```

Now modify the license in the files: Sample-Scene.xml, Sample-Tracking.xml, and Sample-User.xml. Change

```
<License vendor="PrimeSense" key=""/>
```

to:

```
<License vendor="PrimeSense" key="0KOIk2JeIBYClPWVnMoRKn5cdY4="/>
```

Change back to the NITE directory and run the install script.

```
cd ..

sudo ./install.sh
```

That’s it! If you followed steps through to here you should be able to run the sample applications.  The OpenNI samples are here:

```
~/kinect/OpenNI/Platform/Linux/Bin/x64-Release
```

and the PrimeSense samples are here:

```
~/kinect/NITE-Bin-Dev-Linux-x64-v1.5.2.21/Samples/Bin/x64-Release
```

{{< youtube U0ZDe16H82k >}}

Note: if you get the error:

```
InitFromXml failed: Failed to set USB interface!
```

the solution is to remove the gspca_linect kernel module:

```
sudo rmmod gspca_kinect
```

