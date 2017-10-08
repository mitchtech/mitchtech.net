+++
author = "michael"
categories = ["Raspberry Pi","Tutorials"]
comments = true
date = "2012-08-24 00:20:05+00:00"
slug = "raspberry-pi-connect-gmail-facebook-twitter-more"
tags = ["ARM","DIY","Electronics","Facebook","Gmail","Hack","Home Automation","Ifttt","Linux","Python","Raspberry Pi","Twitter","Web Server"]
title = "Easily connect Raspberry Pi to Gmail, Facebook, Twitter & more!"
banner = "img/ifttt.png"

+++

![](/img/ifttt.png)

Easily connect your Raspberry Pi to web services and social networks! This tutorial demonstrates how to painlessly send and receive Gmail on the Raspberry Pi from Python, which in turn, allows you to easily connect it to web services and social networks like Facebook, Twitter, and more! This would normally be well beyond the abilities of most users due to the inherent complexities of programming through social media APis, client/server authentication, etc. However, with the easy-to-use web service Swiss Army knife [ifttt (if this then that)](http://ifttt.com) anyone with even the most basic programming skills can dramatically expand the capabilities of their Raspberry Pi.

#### How does this work?

If you are not yet aware, [ifttt](http://ifttt.com) is a great tool to simplify interaction with many social networks and other web services. It operates with the premise that when some specific action occurs it should perform some other predefined action. The interface is intuitive and very easy to quicky understand. The bridge then is connecting the Raspberry Pi to any of these supported services, which in turn, enables the use of all other services that can respond to that respective trigger. In an earlier  tutorial, I  previously demonstrated how to [connect your Raspberry Pi to your Dropbox account using SSHFS](http://mitchtech.net/dropbox-on-raspberry-pi-via-sshfs/). This is another perfectly viable option to establish two way communication with ifttt. However, instead of using email as the primary communication medium, it relies on Dropbox and the filesystem itself. Depending on your application, this may or may not be a better option.

#### Getting Started

The tutorial uses the most recent Raspbian wheezy image, [(2012-08-16-wheezy-raspbian)](http://www.raspberrypi.org/downloads)but should largely generalize for not only other Raspberry Pi distributions, but most other linux distributions as well (especially those derived from Debian, such as Ubuntu and Mint). The majority of the complexity and functionality comes from the feedparser Python module, which should be available essentially anywhere with Python support, even including Windows and OSX distributions too. In any case, begin by setting up the necessary accounts.

#### Account Setup

As you would undoubtedly expect, the ability to send and receive Gmail is predicated upon having a [Gmail](http://gmail.com) account. You are welcome to use your personal Gmail account if you wish, however, I recommend creating a separate account for the Raspberry Pi as it provides the most flexibility. If you would like to expand beyond the capabilities of Gmail on the Raspberry Pi, you will also need an account on [ifttt](http://ifttt.com). As with Gmail, you can either share your accounts with the Raspberry Pi, or create a separate account specifically for this purpose. Your decision here might be dependent on which services will be necessary for your own specific application.

#### Install Packages

Independent of whether you are using one or multiple Gmail or ifttt accounts, you will first need to install some required packages. Open up a terminal on the Raspberry Pi and install the Python development headers and the pip package manager:

```
sudo apt-get install python-pip python2.7-dev
```

Once that completes, install the feedparser module with the pip package manager:

```
sudo pip install feedparser
```

Now that all of the prerequisites are installed, we can move on to the actual code!

#### Checking Gmail by the Raspberry Pi

This is an example script that will check the Gmail of the specified user, and display the subject line of all unread e-mails.

{{< gist mitchtech 3481728 >}}

#### Sending Gmail from the Raspberry Pi

This is an example script that can be used to send plain text e-mails with Gmail to the specified mail to e-mail address.

{{< gist mitchtech 3481745 >}}

#### Sending Attachments through Gmail from the Raspberry Pi

This is a more complex example script that can be used to attach files to emails sent from Gmail. It sends an array of attached files to an array of recipients.

{{< gist mitchtech 3481781 >}}

#### Scheduling tasks with cron

Often, we want to run tasks at periodic intervals, like to poll Gmail for example. Cron, the UNIX time-based job scheduler, is an easy way to run regular tasks on the Raspberry Pi (or other *nix). Cron is a daemon (like a Web server) that is used to execute commands or scripts automatically at a specified time and date interval. To use it, open the global crontab (cron table) for editing:

```
sudo crontab -e
```

In the text editor, you'll see a commented out section of text describing how to configure tasks with cron. To add your own task, simply add a line to the end of the file. For example, to run the check_gmail.py script above every minute:

```
* * * * * python /home/pi/check_gmail.py
```

Here is a breakdown of what that line actually means, and how you can use to create your own periodic tasks at the desired frequency:

```
* * * * * command to be executed
- - - - -
| | | | |
| | | | |
| | | | +----- day of week (0 - 6) (0 is Sunday, or use names)
| | | +---------- month (1 - 12)
| | +--------------- day of month (1 - 31)
| +-------------------- hour (0 - 23)
+------------------------- min (0 - 59)
```

#### Expanding functionality with ifttt

Now that the Raspberry Pi is capable of both sending and receiving e-mails and running scripts at regular intervals we can move on to fun things! The following are some quick examples of the types of things this interface enables. This list is FAR from inclusive, there are literally thousands of possible combinations!

#### Facebook and Twitter

Update your Facebook status, or post tweets based on raspberry pi events.

![](/img/ifttt-gmail-fb.png)

Alternatively, create a Facebook or Twitter account specifically for the Raspberry Pi, and have it update its own status messages and post its own tweets.

![](/img/ifttt-gmail-twitter.png)

#### Google Calendar

Automatically send alerts for events that match certain criteria within your Google calendar to the Raspberry Pi. Use this to make things like physical notifiers for holidays or other calendar events.

![](/img/ifttt-calendar-gmail.png)

#### SMS and Phone

Receive SMS notifications or phone calls based on events from the Raspberry Pi. Notify based on certain sensor values, or create your own DIY security system, for example.

![](/img/ifttt-gmail-sms.png)

#### Weather and Stocks

It's also easy to control the Raspberry Pi based on the weather forecast. For example, send notifications of impending severe weather or extreme temperatures.

![](/img/ifttt-weather-gmail.png)

Or create physical notifiers that perform actions whenever a specified stock price exceeds or falls below a specified threshold.

![](/img/ifttt-stock-gmail.png)

#### Limitations

There are, of course, a few limitations from using Gmail and cron as the primary basis for communication to the cloud. Cron jobs can only be scheduled at minute granularity, that is, they can be scheduled to occur at maximum frequency of one minute intervals. This is acceptable for most tasks, though it does however leave a bit to be desired for the more 'real time' applications like turning on and off lights, or remotely operated robotics.

