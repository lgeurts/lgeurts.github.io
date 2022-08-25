---
layout: post
title: To-do's when upgrading Ubuntu 20.x to 22.x on a Lenovo ThinkPad X1 Carbon Gen 8
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

<img src="/assets/jammy-jellyfish.png" width="654">

### These are the steps I followed. As usual there is no guarantee but on my laptop it worked like a charm.

### 1 - Check the outut from sudo apt-get update. Does it look similar to what I list below?
---
Hit:1 http://ppa.launchpad.net/atareao/atareao/ubuntu groovy InRelease                                                                             
Hit:2 ***                                                                                           
Ign:3 http://old-releases.ubuntu.com/ubuntu groovy InRelease                                                               
Hit:4 ***                                                        
Ign:5 http://old-releases.ubuntu.com/ubuntu groovy-updates InRelease                                                 
Hit:6 http://ppa.launchpad.net/atareao/atareao/ubuntu focal InRelease
Ign:7 http://old-releases.ubuntu.com/ubuntu groovy-security InRelease                          
Hit:8 ***                                
Err:9 http://old-releases.ubuntu.com/ubuntu groovy Release                                     
  404  Not Found [IP: 91.189.91.124 80]
Hit:10 http://ppa.launchpad.net/audio-recorder/ppa/ubuntu groovy InRelease
Err:11 http://old-releases.ubuntu.com/ubuntu groovy-updates Release      
  404  Not Found [IP: 91.189.91.124 80]
Err:12 http://old-releases.ubuntu.com/ubuntu groovy-security Release     
  404  Not Found [IP: 91.189.91.124 80]
Hit:13 http://ppa.launchpad.net/kubuntu-ppa/backports/ubuntu groovy InRelease
Hit:14 http://ppa.launchpad.net/kubuntu-ppa/backports/ubuntu focal InRelease
Hit:15 http://ppa.launchpad.net/kubuntu-ppa/beta/ubuntu groovy InRelease
Hit:16 http://ppa.launchpad.net/kubuntu-ppa/ppa/ubuntu groovy InRelease
Hit:17 http://ppa.launchpad.net/kubuntu-ppa/ppa/ubuntu focal InRelease
Reading package lists... Done                      '
---
Followed by some jibberisch about updating not being supported e.g. disabled:
---
The repository 'http://old-releases.ubuntu.com/ubuntu groovy Release' does not have a Release file.
Updating from such a repository can't be done securely, and is therefore disabled by default.
See apt-secure(8) manpage for repository creation and user configuration details.
The repository 'http://old-releases.ubuntu.com/ubuntu groovy-updates Release' does not have a Release file.
Updating from such a repository can't be done securely, and is therefore disabled by default.
See apt-secure(8) manpage for repository creation and user configuration details.
The repository 'http://old-releases.ubuntu.com/ubuntu groovy-security Release' does not have a Release file.
Updating from such a repository can't be done securely, and is therefore disabled by default.
See apt-secure(8) manpage for repository creation and user configuration details.
---

### 2 - And does running sudo do-release-upgrade fail with the below error?
---
Please install all available updates for your release before upgrading.
---

### 3 - Then change old-releases back to archive in the sources.list:
---
sudo sed -i "s/old-releases/archive/g" /etc/apt/sources.list /etc/apt/sources.list.d/*.list
---

### 4 - Next add these lines to sources.list:
---
deb http://old-releases.ubuntu.com/ubuntu/ groovy main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ groovy-updates main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ groovy-security main restricted universe multiverse
---

### 5 - Run these commands so you can continue with the update process:
---
sudo apt-get update
sudo apt-get dist-upgrade
sudo do-release-upgrade or sudo update-manager -c
---

### You are done. Enjoy!
