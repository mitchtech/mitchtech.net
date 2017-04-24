+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2013-03-15 07:07:30+00:00"
slug = "raspberry-pi-servo-face-tracker"
tags = ["ARM","Computer Vision","Device Driver","Digital Input","Digital Output","DIY","Electronics","Kernel","LED","Linux","Microcontroller","OpenCV","Pan &amp; Tilt","PWM","Python","Raspberry Pi","Sensor"]
title = "Raspberry Pi OpenCV Pan & Tilt Face Tracker"

+++

{{< youtube WlfecyC1J6A >}}

Create your own face tracking, pan and tilt camera on the Raspberry Pi!

This tutorial will demonstrate use of the OpenCV (computer vision) library to identify and track faces on the raspberry pi using two servos and a USB webcam. For the interested, I previously covered a more thorough overview of the installation of OpenCV from source [here](http://mitchtech.net/raspberry-pi-opencv/), however, I have found that the apt package is sufficient for all but the most bleeding edge of projects.

This project is based on the OpenCV face tracking example that comes along with the source-based distribution. In short, it performs face detection using haar-like features to analyze the video frame, and locates any faces present within it. In the live video window, identified faces are surrounded with a red rectangle. For additional information about how face detection works as well as the specifics of face detection with OpenCV, I recommend [this article by Robin Hewitt](http://www.cognotics.com/opencv/servo_2007_series/part_2/sidebar.html).

Using the coordinates of the rectangle vertices, my script calculates the (X,Y) position of the center of the face. If the face is sufficiently on the left side of the screen, the pan servo will progressively rotate leftward, on the right side, rightward. This is likewise performed for the tilt servo as well, if the face is in the upper portion of the screen, it will pan upward, in the lower portion, pan downward. If the face is detected reasonably within the center of the image, no action is performed by the servos. This prevents unnecessary jitter once the camera has locked itself on the face.

## Hardware

#### Parts needed:

  * 512 MB raspberry pi

  * 2x Hobby servos (Turnigy 9g fom [Hobby King](http://www.hobbyking.com/hobbyking/store/__9549__Turnigy_TG9e_9g_1_5kg_0_10sec_Eco_Micro_Servo.html))

  * Pan & tilt bracket (from [Foxtech FPV](http://www.foxtechfpv.com/plastic-pantilt-for-9g-servos-p-227.html))

  * USB webcam (Microsoft LifeCam Show from [Amazon](http://www.amazon.com/Microsoft-LifeCam-Show-Webcam-Black/dp/B001DWI1F0))

  * Power supply

  * Hook-up wire

  * Raspberry Pi enclosure (from [Built to Spec](http://builttospecstore.storenvy.com/products/745661-clear-raspberry-pi-enclosure-kit))

#### Assembly

Connect the red, power lines of the servos to +5v, the black ground lines to GND, and the yellow signal lines to the desired output pins, GPIO pins 22 and 23 in the example. Here is a diagram of the completed circuit  (created with [Fritzing](http://fritzing.org/)):

[![raspi_servo_facetracker](http://mitchtech.net/wp-content/uploads/2013/01/raspi_servo_facetracker-270x300.png)](http://mitchtech.net/raspberry-pi-servo-face-tracker/raspi_servo_facetracker/)

And here is how it looks all put together:

[![raspi-facetracker-side](http://mitchtech.net/wp-content/uploads/2013/03/raspi-facetracker-side-300x225.jpg)](http://mitchtech.net/raspberry-pi-servo-face-tracker/raspi-facetracker-side/)

[![raspi-facetracker-front](http://mitchtech.net/wp-content/uploads/2013/03/raspi-facetracker-front-225x300.jpg)](http://mitchtech.net/raspberry-pi-servo-face-tracker/raspi-facetracker-front/)

## Software

#### Get the source.

The first step of this procedure is to install the required libraries and packages using the Raspberry Pi package manager. Open up terminal shell and run:

```
sudo apt-get update && sudo apt-get install git python-opencv python-all-dev libopencv-dev
```

This command will pull down all of the required packages (about 215 MB worth) including the git version control system, as well as the OpenCV development headers and Python bindings. The next step is to configure the Raspberry Pi for use with multiple pulse width modulation (PWM) outputs. Normally, the Raspberry Pi has only one channel of PWM output. However, thanks to the efforts of Richard Hirst, eight channels of PWM can be used through the use of this servoblaster kernel driver.The driver creates a device file, /dev/servoblaster to which commands can be sent to control the servos. The commands take the form "=" with servo number representing the desired servo (0-7 in this case) and servo position representing the pulse width in units of 10 µs. For example, to send servo 3 a pulse width of 120 µs: echo 3=120 > /dev/servoblaster To configure the servoblaster on the Raspberry Pi, first pull down the sources from Richard’s Github repo:

```
git clone https://github.com/richardghirst/PiBits.git
```

Then change into the servo blaster directory, and install the module:

```
cd PiBits/ServoBlaster
make install_autostart
```

This command also sets up the necessary udev rules for accessing the /dev/servoblaster device. Note: using the ’install_autostart ’ command will set up a Raspberry Pi to load the servoblaster kernel module on every boot. If you don't want this behavior, execute ‘make install’ instead. In either case, the module will not yet be loaded so go ahead and load it into the kernel using modprobe:

```
sudo modprobe servoblaster
```

Now that all the prerequisites have been installed and the servo blaster device configured, it's time to get the actual face tracking and servo moving code. Clone my repo from Github here:

```
git clone https://github.com/mitchtech/py_servo_facetracker
```

Now change directory into the created folder, and run the script like this:

```
cd py_servo_facetracker
python ./facetracker_servo_gpio.py 0
```

If you have a different servo bracket configuration, the pan and tilt axis may need to be inverted. To do so, invert the sign on the values of panStepSize and tiltStepSize.  Similarly, increasing or decreasing these values will change the sensitivity of the movement, larger numbers corresponding to more degrees moved per face detection frame.

