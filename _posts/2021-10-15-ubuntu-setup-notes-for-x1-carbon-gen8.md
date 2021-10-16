---
layout: post
title: To-do's when (re-)installing Ubuntu 20.x on a Lenovo ThinkPad X1 Carbon Gen 8
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

<img src="/assets/groovy-gorilla.png" width="654">

## BIOS settings

The BIOS has 2 Sleep State options, which you can find in Config > Power > Sleep State. 

The **Linux** option is a traditional S3 power state where all hardware components are turned off except for the RAM, and it should work normally. 

The **Windows** option is a newer software-based "modern standby" which works on Linux (despite the name). One possible benefit to the Windows sleep state is faster wake up time, and one possible drawback is increased power usage. 

## Software packages

Below I list output from my .bash_history and .zsh_history files:
```
$ sudo apt install ubuntu-restricted-extras
$ sudo apt install tmux
$ sudo apt install spotify
$ sudo snap install atom --classic
$ sudo apt install screenfetch
$ sudo apt install curl
$ sudo apt install youtube-dl
$ sudo apt install gimp
$ sudo apt install vim
$ apm install pigments
$ apm install file-icons
$ sudo apt install python
$ snap install powershell --classic
$ apm install teletype
$ sudo apt install git
$ sudo apt install github
$ sudo apt install htop
$ sudo apt install iotop
$ sudo apt install iftop
$ sudo apt install ttyload
$ sudo apt install ranger
$ sudo apt update && sudo apt install virtualbox virtualbox-ext-pack -y
$ sudo apt install steam
$ sudo add-apt-repository ppa:yann1ck/onedrive
$ sudo apt install onedrive
$ sudo apt install ecryptfs-utils cryptsetup
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$ sudo apt install timeshift
$ sudo apt-get remove --purge totem
$ sudo apt install zsh
```
REMINDER: add pmore ackages I usually download

## Possible issues

### Hibernation modus aka deep sleep

In most setups, simply closing the lid will probably trigger deep sleep. If you are using a systemd-based distro, you can verify if it works on the command line:
```
$ systemctl suspend -i
```
### Low cTDP and trip temperature in Linux

This problem is related to 'thermal throttling' on Linux, which is set much below Windows values. It will cause your laptop to run slower than it could when under heavy stress.

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

Check again that the result from running the rdmsr command is 3.

I use a bit lower temperature levels to preserve battery life. If you want to change the values, edit /etc/lenovo_fix, and set the Trip_Temp_C for both battery and AC the way you want:
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

The Lenovo Throttling fix script also supports undervolting. To enable it, edit the /etc/lenovo_fix.conf and update the [UNDERVOLT] section. 

In my case, these settings are stable:

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

There are a lot of theories and advisories about ThinkPad charging thresholds. 
Some say thresholds are needed to keep the battery healthy, some think they are useless and the battery will work the same just as it is.

I always stick with the following settings for my laptops (because they are mostly on AC):

- *Start threshold: 60%*
- *Stop threshold: 65%*

This means that charging will start only if the battery level goes down below 60% and will stop at 65%. This prevents my battery from being charged too often and from being charged beyond a recommended level.

To achieve this for Linux based machines you'll need to install some packages:

```
$ sudo apt-get install tlp tlp-rdw acpi-call-dkms tp-smapi-dkms acpi-call-dkms
```
After that just edit the /etc/default/tlp file and change following values:
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
Note that if you need your laptop fully charged, you can achieve that by running following command while connected to AC:
```
$ tlp fullcharge
```
![](/assets/under-construction.png)
