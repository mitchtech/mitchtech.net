+++
author = "michael"
categories = ["Arduino","Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-15 00:00:55+00:00"
slug = "arduino-on-raspberry-pi"
tags = ["Arduino","ARM","Electronics","Linux","Microcontroller","Raspberry Pi"]
title = "Arduino on Raspberry Pi"
banner = "img/pi-arduino-upload.png"

+++

![](/img/pi-arduino-upload.png)

Connecting an Arduino to a Raspberry Pi is simple. In a terminal, install the Arduino IDE:

```
sudo apt-get install arduino
```

This will take a while to download and install all of the dependencies. Once completed, you can start the IDE from the terminal:

```
arduino
```

Or, from the LXDE menu, Electronics->Arduino IDE. <del>Note: This is IDE version 0018, and does not seem to recognize boards newer then the Duemilanove.</del> Update: The IDE version in the package manager has been updated to version 1.01 and should work with newer boards like the Uno and Leonardo now as well.

The 1 amp power supply I have connected to my Raspberry Pi was not sufficient to power both the Pi and the Arduino through the USB port, so I connected the Arduino through a powered external USB hub. <del>This may not be necessary with a larger power supply connected to the Pi.</del> Update: A larger power supply will not overcome this limitation; the micro USB port on the Raspberry Pi is fused with 1100mA. --Thanks cavebeat

![](/img/pi-arduino.jpg)

Alternatively, the 5V GPIO R_Pi Pin can be used to power the Arduino. Just connect the 5V GPIO pin on the Raspberry Pi to the VIN pin on the Arduino, and respectively GND from one board to the other.

![](/img/raspi-arduino-gpio-power.jpg)

This eliminates the need for the externally powered USB hub, but can make development more of a chore due to the USB port restriction: the keyboard and Arduino will need to be swapped in and out to flash the Arduino.

