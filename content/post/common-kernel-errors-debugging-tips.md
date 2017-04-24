+++
author = "michael"
categories = ["Tutorials","Ubuntu"]
comments = true
date = "2012-05-19 17:51:22+00:00"
layout = "post"
link = "http://mitchtech.net/common-kernel-errors-debugging-tips/"
slug = "common-kernel-errors-debugging-tips"
tags = ["Kernel","Linux","Ubuntu"]
title = "Common Kernel Errors & Debugging Tips"

+++

## Kernel Errors

The following are some typical errors. Some of these may be caught at compilation or link time, and some may only cause problems when you call insmod with the module.

  * division by zero

  * dereferencing a null pointer

  * returning no value or a value other than zero from init_mod

  * calling a C library routine (e.g., malloc() or printf()) from inside a kernel module

Beware that errors in the kernel sometimes have no immediate visible effect, but they may have a delayed effect that is disastrous. This is generally the case if you write garbage into random locations of kernel memory. The location you corrupt may not be referenced to a while. It will be referenced later, and then the effect will occur. Therefore, you cannot assume that the thing you did most recently is necessarily the cause of a crash.

As a consequence, during actual kernel development, one needs to test new kernel code extensively, letting the system run long enough (and with enough other activities going on) to give you confidence that the new code has no harmful side-effects. When you are debugging your own code, if you have tested some code that seems to have gone badly wrong, but not badly enough to crash the system (yet), you may want to reboot the system before testing your revised code. I have seen cases where a system crashed while executing the corrected code, but the crash was because of the delayed effect of damage that had been done by the previously executed (bad) version of the code.

## Kernel Debugging Tips

Here are a few tips to ease kernel development and save some time on repeated reboots.

#### Make Grub Visible

```
sudo vim /etc/default/grub
```

Change this line:

```
GRUB_HIDDEN_TIMEOUT=0
```

to

```
#GRUB_HIDDEN_TIMEOUT=0
```

Then run grub update:

```
sudo update-grub2
```

#### Make Verbose Boot:

```
sudo vim /etc/default/grub
```

Change this line:

```
#GRUB_TERMINAL=console
```

to

```
GRUB_TERMINAL=console
```

Also change this line:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

to

```
GRUB_CMDLINE_LINUX_DEFAULT="debug"
```

Then run grub update:

```
sudo update-grub2
```

#### Text Based Login:

```
sudo vim /etc/default/grub
```

Change this line:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

to

```
GRUB_CMDLINE_LINUX_DEFAULT="text"
```

Then run grub update:

```
sudo update-grub2
```

#### Remove Unnecessary Services (while debugging):

```
sudo apt-get remove apparmor
```

This is a significant savings as far as boot time is concerned.  On my machine, the removal of apparmor reduced the boot-up time  by over 10 seconds.
