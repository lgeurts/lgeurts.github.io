---
layout: post
title: To-do's when upgrading Ubuntu v20.10 to v22.04
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

<img src="/assets/jammy-jellyfish.png" width="654">

These are the steps I followed when upgrading Groovy Gorilla to Jammy Jellyfish. 
Please note that I **can not guarantee** this will work for your setup too. So don't start yelling at this address when your system goes bonkers.
```
$ sudo apt-get update                   
[sudo] password for lgeurts:
-The repository 'http://old-releases.ubuntu.com/ubuntu groovy Release' does not have a Release file.
Updating from such a repository can't be done securely, and is therefore disabled by default.
See apt-secure(8) manpage for repository creation and user configuration details.
The repository 'http://old-releases.ubuntu.com/ubuntu groovy-updates Release' does not have a Release file.
Updating from such a repository can't be done securely, and is therefore disabled by default.
See apt-secure(8) manpage for repository creation and user configuration details.
The repository 'http://old-releases.ubuntu.com/ubuntu groovy-security Release' does not have a Release file.
Updating from such a repository can't be done securely, and is therefore disabled by default.
See apt-secure(8) manpage for repository creation and user configuration details.

$ sudo do-release-upgrade
Please install all available updates for your release before upgrading.

$ sudo sed -i "s/old-releases/archive/g" /etc/apt/sources.list /etc/apt/sources.list.d/*.list

$ echo "[deb http://old-releases.ubuntu.com/ubuntu/ groovy main restricted universe multiverse]" | sudo tee -a /etc/apt/sources.list
$ echo "[deb http://old-releases.ubuntu.com/ubuntu/ groovy-updates main restricted universe multiverse]" | sudo tee -a /etc/apt/sources.list
$ echo "[deb http://old-releases.ubuntu.com/ubuntu/ groovy-security main restricted universe multiverse]" | sudo tee -a /etc/apt/sources.list

$ sudo apt-get update
$ sudo apt-get dist-upgrade
$ sudo do-release-upgrade # sudo update-manager -c
```
The upgrade starts. Once finished, **do not forget to clean up** and check all your apps working!
