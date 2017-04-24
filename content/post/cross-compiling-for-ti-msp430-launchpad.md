+++
author = "meyers"
categories = ["MSP430 Launchpad","Tutorials"]
comments = true
date = "2012-06-23 13:03:13+00:00"
excerpt = "We assumes you are running Ubuntu 12.04 and have a TI msp430g2231 but may work for other msp430 devices (see the Other MSP430 Boards section). This tutorial will cover obtaining the dependencies needed to cross-compile a simple light blinking code for your msp430 device, how to flash the cross-compiled binary to your device, and finish with some advice on how-to compile for other msp430 device variations."
layout = "post"
link = "http://mitchtech.net/cross-compiling-for-ti-msp430-launchpad/"
slug = "cross-compiling-for-ti-msp430-launchpad"
tags = ["blink led","cross-compile","launchpad","msp430","msp430g2231","TI"]
title = "Cross-Compiling for TI MSP430 Launchpad"

+++

[![TI MSP430](http://mitchtech.net/wp-content/uploads/2012/06/IMG_20120623_0916071-300x225.jpg)](http://mitchtech.net/cross-compiling-for-ti-msp430-launchpad/samsung-2/)

Inspired by [this](http://blog.wikifotos.org/2010/11/15/msp430-launchpad-in-ubuntu/) tutorial.

We assumes you are running Ubuntu 12.04 and have a TI msp430g2231 but may work for other msp430 devices (see the _Other MSP430 Boards_ section). This tutorial will cover obtaining the dependencies needed to cross-compile a simple light blinking code for your msp430 device, how to flash the cross-compiled binary to your device, and finish with some advice on how-to compile for other msp430 device variations.

# Packages and Dependencies

```
sudo apt-get install git-core gcc-4.4 texinfo patch libncurses5-dev zlibc zlib1g-dev libx11-dev libusb-dev libreadline6-dev binutils-msp430 gcc-msp430 gdb-msp430 msp430-libc msp430mcu mspdebug srecord libsrecord-dev libgmp-dev
```

If you have gdb installed you will probably get an error like:

```
Unpacking gdb-msp430 (from .../gdb-msp430_7.2~mspgcc-7.2-20110612-1ubuntu1_amd64.deb) ...
dpkg: error processing /var/cache/apt/archives/gdb-msp430_7.2~mspgcc-7.2-20110612-1ubuntu1_amd64.deb (--unpack):
trying to overwrite '/usr/share/gdb/python/gdb/__init__.py', which is also in package gdb 7.4-2012.04-0ubuntu2
```

[Marek Burza](https://bugs.launchpad.net/ubuntu/+source/gdb-msp430/+bug/860045) presents a solution that will force overwrite the existing gdb files with the msp430 version. No worries here because the files are identical.

```
sudo apt-get -o Dpkg::Options::="--force-overwrite" install gdb-msp430
```

Michael ran the above command and had the following error.

```
michael@xt2:~$ sudo apt-get -o Dpkg::Options::="–force-overwrite" install gdb-msp430
Reading package lists... Done
Building dependency tree
Reading state information... Done
You might want to run 'apt-get -f install' to correct these:
The following packages have unmet dependencies:
ia32-libs : Depends: ia32-libs-multiarch but it is not installable
E: Unmet dependencies. Try 'apt-get -f install' with no packages (or specify a solution).
```

The solution is to follow through with the recommended command.

```
sudo apt-get -f install
```

# Code

Save the code below to led.c
{{< gist mitchtech 2978224 >}}

# Compilation

```
msp430-gcc -Os -mmcu=msp430g2553 -o led.elf led.c
```

# Installation

```
sudo mspdebug rf2500
erase
prog led.elf
run
```

# Other MSP430 Boards

To get a list of boards other than the msp430g2231 you can look at the gcc compilation processes in more detail by adding the -v flag.

```
msp430-gcc -v -Os -mmcu=msp430g2553 -o led.elf led.c
```

```
Using built-in specs.
Reading specs from /usr/lib/gcc/msp430/4.5.3/../../../../msp430/lib/msp430mcu.spec
COLLECT_GCC=msp430-gcc
COLLECT_LTO_WRAPPER=/usr/lib/gcc/msp430/4.5.3/lto-wrapper
Target: msp430
Configured with: '/build/buildd/gcc-msp430-4.5.3~mspgcc-20110716/./gcc-4.5.3/configure' -v --enable-languages=c,c++ --prefix=/usr --infodir='/usr/share/info' --mandir='/usr/share/man' --bindir='/usr/bin' --libexecdir='/usr/lib' --libdir='/usr/lib' --enable-shared --with-system-zlib --enable-long-long --enable-nls --without-included-gettext --disable-checking --disable-libssp --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=msp430 --with-pkgversion='GNU GCC patched mspgcc-20110716'
Thread model: single
gcc version 4.5.3 (GNU GCC patched mspgcc-20110716)
COLLECT_GCC_OPTIONS='-v' '-Os' '-mmcu=msp430g2553' '-o' 'led.elf' '-mcpu=430' '-mmpy=none' '-mivcnt=16'
/usr/lib/gcc/msp430/4.5.3/cc1 -quiet -v -D__MSP430G2231__ led.c -mcpu=430 -mmpy=none -mivcnt=16 -quiet -dumpbase led.c -mmcu=msp430g2553 -mcpu=430 -mmpy=none -mivcnt=16 -auxbase led -Os -version -o /tmp/ccxzI5yP.s
GNU C (GNU GCC patched mspgcc-20110716) version 4.5.3 (msp430)
compiled by GNU C version 4.6.2, GMP version 5.0.2, MPFR version 3.1.0-p3, MPC version 0.9
GGC heuristics: --param ggc-min-expand=100 --param ggc-min-heapsize=131072
ignoring nonexistent directory "/usr/lib/gcc/msp430/4.5.3/../../../../msp430/sys-include"
#include "..." search starts here:
#include search starts here:
/usr/lib/gcc/msp430/4.5.3/include
/usr/lib/gcc/msp430/4.5.3/include-fixed
/usr/lib/gcc/msp430/4.5.3/../../../../msp430/include
End of search list.
GNU C (GNU GCC patched mspgcc-20110716) version 4.5.3 (msp430)
compiled by GNU C version 4.6.2, GMP version 5.0.2, MPFR version 3.1.0-p3, MPC version 0.9
GGC heuristics: --param ggc-min-expand=100 --param ggc-min-heapsize=131072
Compiler executable checksum: f3faedb94e9b3def3d948861a0f5d178
COLLECT_GCC_OPTIONS='-v' '-Os' '-mmcu=msp430g2553' '-o' 'led.elf' '-mcpu=430' '-mmpy=none' '-mivcnt=16'
/usr/lib/gcc/msp430/4.5.3/../../../../msp430/bin/as -mcpu=430 -mmcu=msp430g2553 -o /tmp/ccISTyMA.o /tmp/ccxzI5yP.s
COMPILER_PATH=/usr/lib/gcc/msp430/4.5.3/:/usr/lib/gcc/msp430/4.5.3/:/usr/lib/gcc/msp430/:/usr/lib/gcc/msp430/4.5.3/:/usr/lib/gcc/msp430/:/usr/lib/gcc/msp430/4.5.3/../../../../msp430/bin/
LIBRARY_PATH=/usr/lib/gcc/msp430/4.5.3/:/usr/lib/gcc/msp430/4.5.3/../../../../msp430/lib/
COLLECT_GCC_OPTIONS='-v' '-Os' '-mmcu=msp430g2553' '-o' 'led.elf' '-mcpu=430' '-mmpy=none' '-mivcnt=16'
/usr/lib/gcc/msp430/4.5.3/collect2 -m msp430 -o led.elf /usr/lib/gcc/msp430/4.5.3/crt0ivtbl16.o -L/usr/lib/gcc/msp430/4.5.3 -L/usr/lib/gcc/msp430/4.5.3/../../../../msp430/lib /tmp/ccISTyMA.o -lgcc -lc -lgcc -lcrt0 -L /usr/lib/gcc/../../msp430/lib/ldscripts/msp430g2231/
```

From the gcc output we can see can further examine any one of the many linked in libraries. Lets look at /usr/lib/gcc/../../msp430/lib/ldscripts/msp430g2231/ for example.

```
cd /usr/lib/gcc/../../msp430/lib/ldscripts/msp430g2231/
ls
cd ..
ls -al
```

```
drwxr-xr-x 2 root root 4096 Jun 23 08:13 cc430f5133
drwxr-xr-x 2 root root 4096 Jun 23 08:13 cc430f5135
drwxr-xr-x 2 root root 4096 Jun 23 08:13 cc430f5137
drwxr-xr-x 2 root root 4096 Jun 23 08:13 cc430f6125
drwxr-xr-x 2 root root 4096 Jun 23 08:13 cc430f6126
drwxr-xr-x 2 root root 4096 Jun 23 08:13 cc430f6127
drwxr-xr-x 2 root root 4096 Jun 23 08:13 cc430f6135
drwxr-xr-x 2 root root 4096 Jun 23 08:13 cc430f6137
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430afe221
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430afe222
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430afe223
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430afe231
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430afe232
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430afe233
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430afe251
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430afe252
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430afe253
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430bt5190
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c091
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c092
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c111
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c1111
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c112
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c1121
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c1331
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c1351
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c311s
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c312
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c313
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c314
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c315
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c323
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c325
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c336
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c337
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c412
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430c413
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430cg4616
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430cg4617
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430cg4618
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430cg4619
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430e112
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430e313
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430e315
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430e325
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430e337
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f110
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1101
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1101a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1111
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1111a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f112
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1121
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1121a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1122
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1132
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f122
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1222
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f123
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1232
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f133
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f135
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f147
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1471
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f148
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1481
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f149
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1491
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f155
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f156
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f157
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1610
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1611
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f1612
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f167
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f168
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f169
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2001
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2002
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2003
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2011
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2012
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2013
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2101
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2111
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2112
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2121
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2122
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2131
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2132
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2232
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2234
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2252
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2254
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2272
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2274
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f233
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2330
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f235
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2350
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2370
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2410
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2416
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2417
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2418
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2419
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f247
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2471
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f248
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2481
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f249
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2491
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2616
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2617
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2618
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f2619
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f412
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f413
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4132
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f415
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4152
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f417
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f423
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f423a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f425
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4250
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f425a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4260
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f427
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4270
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f427a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f435
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4351
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f436
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4361
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f437
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4371
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f438
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f439
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f447
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f448
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4481
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f449
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4491
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4616
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f46161
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4617
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f46171
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4618
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f46181
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4619
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f46191
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47126
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47127
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47163
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47166
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47167
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47173
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47176
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47177
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47183
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47186
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47187
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47193
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47196
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f47197
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f477
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f478
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4783
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4784
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f479
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4793
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f4794
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5131
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5132
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5151
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5152
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5171
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5172
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5304
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5308
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5309
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5310
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5324
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5325
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5326
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5327
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5328
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5329
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5340
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5341
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5342
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5418
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5418a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5419
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5419a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5435
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5435a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5436
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5436a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5437
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5437a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5438
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5438a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5500
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5501
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5502
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5503
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5504
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5505
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5506
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5507
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5508
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5509
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5510
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5513
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5514
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5515
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5517
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5519
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5521
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5522
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5524
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5525
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5526
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5527
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5528
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5529
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5630
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5631
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5632
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5633
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5634
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5635
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5636
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5637
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f5638
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f6630
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f6631
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f6632
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f6633
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f6634
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f6635
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f6636
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f6637
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430f6638
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe423
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe4232
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe423a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe4242
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe425
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe4252
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe425a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe427
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe4272
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fe427a
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg4250
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg4260
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg4270
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg437
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg438
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg439
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg4616
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg4617
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg4618
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg4619
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg477
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg478
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fg479
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fr5720
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fr5725
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fr5728
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fr5729
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fr5730
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fr5735
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fr5738
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fr5739
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fw423
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fw425
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fw427
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fw428
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430fw429
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2001
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2101
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2102
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2111
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2112
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2113
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2121
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2131
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2132
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2152
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2153
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2201
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2202
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2203
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2211
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2212
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2213
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2221
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2231
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2232
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2233
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2252
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2253
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2302
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2303
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2312
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2313
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2332
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2333
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2352
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2353
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2402
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2403
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2412
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2413
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2432
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2433
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2452
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2453
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2513
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2533
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430g2553
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430l092
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430p112
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430p313
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430p315
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430p315s
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430p325
drwxr-xr-x 2 root root 4096 Jun 23 08:13 msp430p337
```

It seems that the ubuntu msp430 cross-compiler packages include support for many variation of the msp430. To cross-compile for these variations, adjust the -mmcu=msp430 flag accordingly and, in the led.c file, alter the #include file to reflect the chosen board.
