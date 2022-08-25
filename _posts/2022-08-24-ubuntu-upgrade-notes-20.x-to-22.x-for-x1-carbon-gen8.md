---
layout: post
title: To-do's when upgrading Ubuntu 20.x to 22.x on a Lenovo ThinkPad X1 Carbon Gen 8
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

<img src="/assets/jammy-jellyfish.png" width="654">

These are the steps I followed when upgrading Groovy Gorilla to Jammy Jellyfish. Note that I can not guarantee it will work for your setup too. So don't start yelling.

1 - Running sudo-apt-update, do you get these results?
```
-The repository 'http://old-releases.ubuntu.com/ubuntu groovy Release' does not have a Release file.
Updating from such a repository can't be done securely, and is therefore disabled by default.
See apt-secure(8) manpage for repository creation and user configuration details.
The repository 'http://old-releases.ubuntu.com/ubuntu groovy-updates Release' does not have a Release file.
Updating from such a repository can't be done securely, and is therefore disabled by default.
See apt-secure(8) manpage for repository creation and user configuration details.
The repository 'http://old-releases.ubuntu.com/ubuntu groovy-security Release' does not have a Release file.
Updating from such a repository can't be done securely, and is therefore disabled by default.
See apt-secure(8) manpage for repository creation and user configuration details.
```
2 - And does sudo do-release-upgrade fail with this error?
```
Please install all available updates for your release before upgrading.
```
3 - First, let's change old-releases back to archive in the sources.list:
```
sudo sed -i "s/old-releases/archive/g" /etc/apt/sources.list /etc/apt/sources.list.d/*.list
```
4 - Next add these lines to sources.list:
```
deb http://old-releases.ubuntu.com/ubuntu/ groovy main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ groovy-updates main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ groovy-security main restricted universe multiverse
```
5 - Run these commands so you can continue with the update process:
```
sudo apt-get update
sudo apt-get dist-upgrade
sudo do-release-upgrade or sudo update-manager -c
```
The upgrade starts and you are done. Enjoy!
