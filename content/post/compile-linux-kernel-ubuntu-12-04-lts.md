+++
author = "michael"
categories = ["Tutorials","Ubuntu"]
comments = true
date = "2012-05-19 17:39:47+00:00"
slug = "compile-linux-kernel-ubuntu-12-04-lts"
tags = ["Kernel","Linux","Ubuntu"]
title = "Compile Linux Kernel on Ubuntu 12.04 LTS"

+++

This tutorial will outline the process to compile your own kernel for Ubuntu. It will demonstrate both the traditional process using 'make' and 'make install' as well as the Debian method, using 'make-dpkg'. This is a quick overview of the compilation process, for a more thourough walkthrough, see [Compile Linux Kernel on Ubuntu 12.04 LTS (Detailed)](http://mitchtech.net/compile-linux-kernel-on-ubuntu-12-04-lts-detailed/).  In both cases, we begin by installing some dependencies:

```
sudo apt-get install git-core libncurses5 libncurses5-dev libelf-dev asciidoc binutils-dev linux-source qt3-dev-tools libqt3-mt-dev libncurses5 libncurses5-dev fakeroot build-essential crash kexec-tools makedumpfile kernel-wedge kernel-package
```

Note: qt3-dev-tools and libqt3-mt-dev is necessary if you plan to use 'make xconfig' and libncurses5 and libncurses5-dev  if you plan to use 'make menuconfig'.  Next, copy the kernel sources with wget:

```
wget http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.2.17.tar.bz2
```

Extract the archive and change into the kernel directory:

```
tar -xjvf linux-3.2.17.tar.bz2 cd linux-3.2.17/
```

Now you are in the top directory of a kernel source tree. Before building the kernel, you must configure it. If you wish to re-use the configuration of your currently running kernel, start by copying the current config contained in /boot:

```
cp -vi /boot/config-`uname -r` .config
```

Parse the .config file using make with the oldconfig flag.  If there are new options available in the downloaded kernel tree, you may be prompted to make a selection to include them or not.  If unsure, press enter to accept the defaults.

```
make oldconfig
```

Since the 2.6.32 kernel, a new feature allows you to update the configuration to only compile modules that are actually used in your system. As above, make selections if prompted, otherwise hit enter for the defaults.

```
make localmodconfig
```

Now you can configure the build with ncurses using the 'menuconfig' flag:

```
make menuconfig
```

or, using a GUI with the 'xconfig' flag:

```
make xconfig
```

Now we are ready to start the build. You can speed up the compilation process by enabling parallel make with the -j flag. The recommended use is 'processor cores + 1', e.g. 5 if you have a quad core processor:

```
make -j5
```

Once the initial compilation has completed, install the dynamically loadable kernel modules:

```
sudo make modules_install
```

Finally, install the kernel:

```
sudo make install
```

## Debian Method:

Instead of the compilation process of above, you can alternatively compile the kernel as installable .deb packages. This improves the portability of the kernel, since installation on a different machine is as simple as installing the packages. Rather than using 'make' and 'make install', we use 'make-kpkg':

```
fakeroot make-kpkg --initrd --append-to-version=-some-string-here kernel-image kernel-headers
```

Unlike above, you cannot enable parallel compilation with make-kpkg using the -j flag. Instead, define the CONCURRENCY_LEVEL environment variable.

```
export CONCURRENCY_LEVEL=3
```

Once the compilation has completed, you can install the kernel and kernel headers using dpkg:

```
sudo dpkg -i linux-image-3.2.14-mm_3.2.14-mm-10.00.Custom_amd64.deb

sudo dpkg -i linux-headers-3.2.14-mm_3.2.14-mm-10.00.Custom_amd64.deb
```
