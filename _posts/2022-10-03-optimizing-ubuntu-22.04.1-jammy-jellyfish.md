---
layout: post
title: Optimizing Ubuntu 22.04.1 Jammy Jellyfish
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

## Introduction
These tips are meant for Ubuntu systems, but in general any Debian based distro should be good for go.
Keep in mind that, as everything in life, nothing comes for free. Every optimization has its own pricetag and you must decide how much you are willing to pay for it.

### Lower swappiness (dismiss when having more than 16 Gb RAM)
When working with limited RAM, Ubuntu will aggressively try to free memory to enlarge the caches aka swapping. This leads to a lot of write actions to your SSD which in their turn slow down your system and chip away chunks of a disk's total lifetime.
Ubuntu's standard [swap_tendency](https://unix.stackexchange.com/questions/134202/when-is-swap-triggered-or-how-to-calculate-swap-tendency#134206) setting never was that optimal (more info is found [here](https://rudd-o.com/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that)) and needs adjusting.

Open your terminal and query the current swappiness value by typing:
```
$ cat /proc/sys/vm/swappiness
```
Probably swappiness wil return a value of 60 which is too high for normal use. To lower swap_tendency to a more appropriate value:
```
$ gedit admin:///etc/sysctl.conf
```
The Text Editor app will open. At the end of the file type:
```
# Lower swap_tendency
vm.swappiness=25
```
and save. To activate the new setting, restart the computer.

### Activate the zram system kernel function

If your PC has enough memory, zram could be used to replace the /swap.img file altogether. 

Enabling zram causes conflicts with zswap, which is enabled by default. Disable it by typing the following command in your terminal:
```
$ echo 0 > /sys/module/zswap/parameters/enabled
```
Now we can load the zram module:
```
$ modprobe zram
```
We should find a device node named /dev/zram0. Let’s allocate a size for it:
```
$ echo 800M > /sys/block/zram0/disksize # Change size to your liking
```
Format this new device as if it was just a normal disk partition we designated for swap:
```
$ mkswap --label zram0 /dev/zram0
$ swapon -p 100 /dev/zram0
```
To set zram permanently, once again run gedit and add or change following lines in /etc/default/grub:
```
GRUB_CMDLINE_LINUX_DEFULT=""
GRUB_CMDLINE_LINUX="zswap.enabled=0"
```
Save the file and run:
```
$ update-grub 
```
to update the bootloader config files.

Now, we make sure the zram module is loaded at boot and knows the number of devices we need:
```
$ echo "zram" > /etc/modules-load.d/zram.conf
$ echo "options zram num_devices=1" > /etc/modprobe.d/zram.conf
```
Create a udev rule so that our device node is formatted automatically as swap:
```
$ sudo -i
$ root@yourmachinename:~# cat > /etc/udev/rules.d/99-zram.rules KERNEL=="zram0", ATTR{disksize}="800M" RUN="/usr/sbin/mkswap -L zram0 /dev/zram0", TAG+="systemd"
```






