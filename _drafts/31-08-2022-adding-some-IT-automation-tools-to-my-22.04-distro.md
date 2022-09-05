---
layout: post
title: Adding some IT automation tools to my 22.04 box
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

## Docker and Docker-Compose

Docker compose > todo.

## Podman and Podman Desktop

## Vagrant


```
$ sudo apt-get update                   
[sudo] password for lgeurts:
# You should see output similar to this.
E: The repository 'http://old-releases.ubuntu.com/ubuntu groovy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
E: The repository 'http://old-releases.ubuntu.com/ubuntu groovy-updates Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
E: The repository 'http://old-releases.ubuntu.com/ubuntu groovy-security Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.

# Next test, spewing more jibberish.
$ sudo do-release-upgrade
Please install all available updates for your release before upgrading.

# Clean the apt cache.
$ sudo rm -rf /var/lib/apt/lists/*

# Replace entries in sources files. 
$ sudo sed -i "s/old-releases/archive/g" /etc/apt/sources.list /etc/apt/sources.list.d/*.list

# These 3 echo commands are for making sure you really have the correct entries even the above should have done the trick.
# Can also use any editor you want if that makes you feel more comfy.
$ echo "[deb http://old-releases.ubuntu.com/ubuntu/ groovy main restricted universe multiverse]" | sudo tee -a /etc/apt/sources.list
$ echo "[deb http://old-releases.ubuntu.com/ubuntu/ groovy-updates main restricted universe multiverse]" | sudo tee -a /etc/apt/sources.list
$ echo "[deb http://old-releases.ubuntu.com/ubuntu/ groovy-security main restricted universe multiverse]" | sudo tee -a /etc/apt/sources.list

# Kick it.
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get dist-upgrade # do-release does this again.
$ sudo apt install update-manager-core
$ sudo do-release-upgrade
```