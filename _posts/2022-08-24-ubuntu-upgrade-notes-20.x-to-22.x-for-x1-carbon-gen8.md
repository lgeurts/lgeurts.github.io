---
layout: post
title: To-do's when upgrading Ubuntu EOL 20.10 to 22.04.1
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

<img src="/assets/jammy-jellyfish.png" width="654">

These are the steps I followed when upgrading Groovy Gorilla to Jammy Jellyfish. 
Please note that **I cannot guarantee this will work** for your setup too. So don't start yelling at this address when your system goes bonkers. :(

### Start coomand block
```
$ sudo apt-get update                   
[sudo] password for lgeurts:
E: The repository 'http://old-releases.ubuntu.com/ubuntu groovy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
E: The repository 'http://old-releases.ubuntu.com/ubuntu groovy-updates Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
E: The repository 'http://old-releases.ubuntu.com/ubuntu groovy-security Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.

$ sudo do-release-upgrade
Please install all available updates for your release before upgrading.

$ sudo sed -i "s/old-releases/archive/g" /etc/apt/sources.list /etc/apt/sources.list.d/*.list 

# These 3 echo commands are for making sure you really have the correct entries even the above should have done the trick. 
$ echo "[deb http://old-releases.ubuntu.com/ubuntu/ groovy main restricted universe multiverse]" | sudo tee -a /etc/apt/sources.list
$ echo "[deb http://old-releases.ubuntu.com/ubuntu/ groovy-updates main restricted universe multiverse]" | sudo tee -a /etc/apt/sources.list
$ echo "[deb http://old-releases.ubuntu.com/ubuntu/ groovy-security main restricted universe multiverse]" | sudo tee -a /etc/apt/sources.list

$ sudo apt-get update
$ sudo apt-get dist-upgrade # Next command will run this anyways.
$ sudo do-release-upgrade # Can also use sudo update-manager -c
```
### End command block

The upgrade starts. Once finished, **do not forget to clean up and check those apps**!
