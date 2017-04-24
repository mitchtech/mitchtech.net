+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2012-06-08 04:03:32+00:00"
slug = "raspberry-pi-apache"
tags = ["Apache","Linux","Raspberry Pi","Web Server"]
title = "Raspberry Pi + Apache"

+++

[![](http://mitchtech.net/wp-content/uploads/2012/06/pi-apache-300x183.png)](http://mitchtech.net/raspberry-pi-apache/pi-apache/)
Its quite easy to install the Apache web server on the Raspberry Pi. This process assumes you have Debian for Raspberry Pi installed on an SD card. If not, see [RPi Easy SD card setup](http://elinux.org/RPi_Easy_SD_Card_Setup). Open a terminal (or login via SSH) and install the package with apt-get:

```
sudo apt-get install apache2
```

**UPDATE: 9/18/12: The following group creation error appears to have been corrected in an updated package and should no longer be necessary.  **

However, the install will not complete successfully:

```
Setting up apache2-mpm-worker (2.2.16-6+squeeze7) ...
Starting web server: apache2apache2: bad group name www-data
Action 'start' failed.
The Apache error log may have more information.
failed!
invoke-rc.d: initscript apache2, action "start" failed.
```

While the errors suggests that the Apache error log may have more information... it does not! However, bad group name is a clue. For some reason, apache user www-data gets created correctly, but the apache group does not. This is corrected by the following actions:

```
sudo addgroup www-data
sudo usermod -a -G www-data www-data
```

And then restart the apache web server:

```
sudo /etc/init.d/apache2 restart
```

That's it! You can confirm that it is working by opening a browser and navigating to the web server root. To do this locally on the Raspberry Pi, open up a web browser such as Midori, the pre-installed browser on the Debian image, and navigate to:

```
http://127.0.0.1/
```

Alternatively, navigate from a browser on another machine on your local network, only substitute the local address of the Raspberry Pi. To find the address of the Raspberry Pi, open a terminal and run:

```
ifconfig
```

Then navigate to the corresponding IP address of the Pi.

