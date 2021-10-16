---
layout: post
title: List of issues when installing Ubuntu 20.10 on a Lenovo ThinkPad X1 Carbon Gen 8
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

These notes were written to **help me out** should I ever have to re-install Groovy Gorilla. 

Note: You'll probably ask why I am using an older distro. Despite being out of support I see no reason to upgrade (yet). New features? Latest Gnome? Don't need them. Security? I mostly work offline and for those few times I want to read mail or talk in Slack with my teammates, my trusted firewall should be enough. Social media, web-browsing, gaming, any activities bearing a risk of getting infected or hacked, are restricted to a sandboxed Windows 10 installation containing no private data whatsoever. Issues? Wipe and reload.

So, now you know, let's get on with it.

<!--- <img src="/assets/groovy-gorilla.jpg" width="360"> --->

## Possible issues

### Hibernation modus aka deep sleep

In most setups, simply closing the lid will probably trigger deep sleep. If you're using a systemd-based distribution (most of which are), you can also verify if it works on the command line:
```
$ systemctl suspend -i
```
### Low cTDP and trip temperature in Linux

This problem is related to thermal throttling on Linux, that is set much below the Windows values. This will cause your laptop to run much slower than it could under heavy stress.

Before you attempt to apply this solution, please make sure that the problem still exists when you read it. To do so, open a Linux terminal and run following commands:
```
$ sudo apt-get install msr-tools
$ sudo rdmsr -f 29:24 -d 0x1a2
```
If you see 3 as a result value (or 15 when running on battery), you don’t have to do anything. Otherwise:
1. Disable Secure Boot in the BIOS (won’t work otherwise)
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
Check again, that the result from running the rdmsr command is 3

Personally, I use a bit lower temperature levels to preserve battery life in favor of performance. If you want to change the default values, you need to edit the /etc/lenovo_fix file and set the Trip_Temp_C for both battery and AC the way you want:
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

The amazing Lenovo Throttling fix script supports undervolting. To enable it, please edit the /etc/lenovo_fix.conf and update the [UNDERVOLT] section. In my case, these settings are stable:

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

There are a lot of theories and information about ThinkPad charging thresholds. Some theories say thresholds are needed to keep the battery healthy, some think they are useless and the battery will work the same just as it is. In this article I will try not to settle that argument. 🙂 Instead I try to tell how and why I use them, and then proceed to show how they can be changed in different versions of Windows, should you still want to change these thresholds.

I always stick with following settings for my laptops (and somehow I feel that it works):

- Start threshold: 45%
- Stop threshold: 95%

This means that the charging will start only if the battery level goes down below 45% and will stop at 95%. This prevents battery from being charged too often and from being charged beyond a recommended level.

To achieve this for Linux based machines you need to install some packages by running:

```
$ sudo apt-get install tlp tlp-rdw acpi-call-dkms tp-smapi-dkms acpi-call-dkms
```

After that just edit the /etc/default/tlp file and edit following values:
```
# Uncomment both of them if commented out
START_CHARGE_THRESH_BAT0=45
STOP_CHARGE_THRESH_BAT0=95
```

Reboot, run:
```
sudo tlp-stat | grep tpacpi-bat
```

and check if the values are as you expect:
```
tpacpi-bat.BAT0.startThreshold          = 45 [%]
tpacpi-bat.BAT0.stopThreshold           = 95 [%]
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
