---
layout: post
title: To-do's when re-installing Ubuntu 20.x on a Lenovo ThinkPad X1 Carbon Gen 8
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

<!--- <img src="/assets/groovy-gorilla.jpg" width="360"> --->

## Software packages

## Possible issues

### Hibernation modus aka deep sleep

In most setups, simply closing the lid will probably trigger deep sleep. If you are using a systemd-based distro, you can verify if it works on the command line:
```
$ systemctl suspend -i
```
### Low cTDP and trip temperature in Linux

This problem is related to **thermal throttling** on Linux, which is set much below Windows values. It will cause your laptop to run slower than it could when under heavy stress.

Before attempting to apply this solution, please make sure that the problem still exists. To do so, open a Linux terminal and run following commands:
```
$ sudo apt-get install msr-tools
$ sudo rdmsr -f 29:24 -d 0x1a2
```
If you see 3 as a result value (15 when running on the battery), you don’t have to do anything. Otherwise:
1. Disable Secure Boot in the BIOS (won’t work otherwise);
2. Run this command:
```
sudo apt install git virtualenv build-essential python3-dev \
  libdbus-glib-1-dev libgirepository1.0-dev libcairo2-dev
```
3. Install lenovo-throttling-fix:
```
$ cd lenovo-throttling-fix/
$ sudo ./install.sh
```

Check again, that the result from running the rdmsr command is 3.

Personally, I use a bit lower temperature levels to preserve battery life in favor of performance. If you want to change values, edit the /etc/lenovo_fix file and set the Trip_Temp_C for both battery and AC the way you want:
```
[BATTERY]
# Other options here...
PL2_Tdp_W: 40
Trip_Temp_C: 75

[AC]
# Other options here...
PL1_Tdp_W: 34
PL2_Tdp_W: 40
Trip_Temp_C: 90
```
## CPU undervolting

The Lenovo Throttling fix script supports undervolting. To enable it, edit the /etc/lenovo_fix.conf and update the [UNDERVOLT] section. In my case, these settings are stable:

```
[UNDERVOLT]
# CPU core voltage offset (mV)
CORE: -110
# Integrated GPU voltage offset (mV)
GPU: -90
# CPU cache voltage offset (mV)
CACHE: -110
# System Agent voltage offset (mV)
UNCORE: -90
# Analog I/O voltage offset (mV)
ANALOGIO: 0
```
## Battery charging thresholds

There are a lot of theories and information about ThinkPad charging thresholds. Some theories say thresholds are needed to keep the battery healthy, some think they are useless and the battery will work the same just as it is.

I always stick with following settings for my laptops (because they are msotly on AC):

- Start threshold: 60%
- Stop threshold: 65%

This means that the charging will start only if the battery level goes down below 60% and will stop at 65%. This prevents battery from being charged too often and from being charged beyond a recommended level.

To achieve this for Linux based machines you need to install some packages by running:

```
$ sudo apt-get install tlp tlp-rdw acpi-call-dkms tp-smapi-dkms acpi-call-dkms
```
After that just edit the /etc/default/tlp file and edit following values:
```
# Uncomment both of them if commented out
START_CHARGE_THRESH_BAT0=60
STOP_CHARGE_THRESH_BAT0=65
```
Reboot, run:
```
sudo tlp-stat | grep tpacpi-bat
```
and check if the values are as you expect:
```
tpacpi-bat.BAT0.startThreshold          = 60 [%]
tpacpi-bat.BAT0.stopThreshold           = 65 [%]
```
You can change these thresholds anytime, and apply changes using command:
```
$ sudo tlp start
```
Note, that if you need to have your laptop fully charged, you can achieve that by running following command while connected to AC:
```
$ tlp fullcharge
```
![](/assets/under-construction.png)
