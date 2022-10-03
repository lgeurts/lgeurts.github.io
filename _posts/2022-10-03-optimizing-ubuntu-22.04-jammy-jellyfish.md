---
layout: post
title: Optimizing Ubuntu 22.04 Jammy Jellyfish
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

## Introduction
These tips are meant for Ubuntu systems, but in general any Debian based distro should be good to go.
Keep in mind that, as everything in life, nothing comes for free. Making one part faster will have a "small" negative impact on other components.

## List of commands
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
