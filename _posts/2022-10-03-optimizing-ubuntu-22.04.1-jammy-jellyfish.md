---
layout: post
title: Optimizing Ubuntu 22.04.1 Jammy Jellyfish
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

These tips are meant for Ubuntu systems, but in general any Debian based distro should be ready to go.
Keep in mind that, as everything in life, nothing comes for free. Every optimization has its own pricetag and you must decide how much you are willing to pay for it.

## Burning my disk, no more ...

### The Firefox sessionstore

Sessionstore is responsible for caching which pages were already opened should Firefox suddenly crash. While this is a great feature (you reopen all lost tabs and continue browsing), it causes a lot of writes to your SSD. 

Disabling is really easy. Type about:config in de addressbar and press Enter. Click on agree and look for sessionstore. Double-click on browser.sessionstore.interval and change 15000 (15 seconds) to 15000000. Press OK, restart Firefox.

### Swappiness (dismiss when having more than 16 Gb RAM)
When working with limited RAM, Ubuntu will aggressively try to free memory to enlarge the caches aka swapping. This again will lead to large quantities of write actions on your SSD which in their turn slow down your system and chip away at the disk's total lifetime.

To change Ubuntu's standard [swap_tendency](https://unix.stackexchange.com/questions/134202/when-is-swap-triggered-or-how-to-calculate-swap-tendency#134206) weight, open a terminal and query the current swappiness value by typing:
```
$ cat /proc/sys/vm/swappiness
```
Probably swappiness wil return a value of 60 which is too high for normal use. Let's edit the configuration file:
```
$ gedit admin:///etc/sysctl.conf
```
The text editor app will open. At the end type:
```
# Lower swap_tendency
vm.swappiness=25
```
and save. To activate the new setting, restart the computer.

## Faster, faster, performance is key

### Move /tmp to tempfs

Another trick to make a machine run faster is moving /tmp to tmpfs. Temporary files will no longer be placed on the physical disk but in a virtual RAM disk. 

Open a terminal and type:
```
$ sudo cp -v /usr/share/systemd/tmp.mount /etc/systemd/system/
$ sudo systemctl enable tmp.mount
```
Reboot the computer.

Should you experience issues, you can always undo the change by typing:
```
$ sudo rm -v /etc/systemd/system/tmp.mount
```

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
$ echo 1024M > /sys/block/zram0/disksize # change size to your liking.
```
Format that new device as if it was just a normal disk partition we designated for swap:
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

Now, we make sure the zram module is loaded at boot, and knows the number of devices we need (if we were also using zram for other tmpfs directories like /tmp, we’d have to increase the number):
```
$ echo "zram" > /etc/modules-load.d/zram.conf
$ echo "options zram num_devices=1" > /etc/modprobe.d/zram.conf
```
Create a udev rule so that the device node is formatted automatically as swap:
```
$ sudo -i
$ [sudo] password for **my username**:
$ root@yourmachinename:~# cat > /etc/udev/rules.d/99-zram.rules KERNEL=="zram0", ATTR{disksize}="1024M" RUN="/usr/sbin/mkswap -L zram0 /dev/zram0", TAG+="systemd"
```
Add the device to /etc/fstab. Additionally, we can give the pri=value as an option to the swap entry:
```
$ sudo -i
$ [sudo] password for **my username**:
$ root@yourmachinename:~# printf "/dev/zram0\tnone\tswap\tdefaults,pri=100\t0\t0\n" >> /etc/fstab
$ root@yourmachinename:~# tail /etc/fstab # to check the output.
```
Reboot and verify that our swap device is active:
```
$ history | tail -n 2
$ swapon
```

### Lower the pressure on the inode cache

If your PC has has enough free RAM available, you can also achieve a little more performance by lowering the tendency on reclaiming the memory which is used for caching of directory and inode objects. 

Warning, clearing cache less frequently can impact new processes trying to load (bad_address or address_in_use). 

Open your terminal and type:
```
$ gedit admin:///etc/sysctl.conf
```
Our text editor opens. Add following lines to the config file:
```
# Customize cache management
vm.vfs_cache_pressure=50
```
and save. This setting will be activated after rebooting your computer.

*These are just some tips I think are useful. Should something be missing or you have an item that belongs in this list, please let me know by mail.*

*Ref: Web: [zram: Compressed RAM based block devices](https://www.kernel.org/doc/html/v5.3/admin-guide/blockdev/zram.html) - Kernel.org.*
