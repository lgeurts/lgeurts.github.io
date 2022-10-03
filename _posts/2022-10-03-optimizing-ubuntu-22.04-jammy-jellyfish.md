---
layout: post
title: Optimizing Ubuntu 22.04 Jammy Jellyfish
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
Ubuntu's standard [swap_tendency](https://unix.stackexchange.com/questions/134202/when-is-swap-triggered-or-how-to-calculate-swap-tendency#134206) is not optimal (more info found [here](https://rudd-o.com/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that)) and needs adjusting.

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

Zram can be used to replace the /swap.img file alltogether. Enabling zram could cause conflicts with zswap, which is enabled by default. 

Disable it by typing the following command in your terminal:
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
Format this new device as if it was just a normal disk partiition we designated for swap:
```
$ mkswap --label zram0 /dev/zram0
$ swapon -p 100 /dev/zram0
```
To set zram permanently open gedit again and add/change the following lines in /etc/default/grub:
```
GRUB_CMDLINE_LINUX_DEFULT=""
GRUB_CMDLINE_LINUX="zswap.enabled=0"
```
Save the file and run:
```
$ update-grub 
```
to update the bootloader config files.







