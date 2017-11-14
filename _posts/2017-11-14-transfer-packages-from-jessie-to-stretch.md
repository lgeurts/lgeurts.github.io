---
layout: post
title: How to transfer a package list from Jessie to Stretch
read_time: true  
comments: true
category: Open Source
tags: [ Debian Linux ] 
---

List the currently installed packages, save them to a file 'my-packages' and then read that file to re-install:

```$ dpkg -l | grep ^ii | awk '{print $2}' > my-packages```

In your newly installed Debian-based distro, install the saved packages:

```$ sudo apt-get install $(cat my-packages)```

Or get [apt-clone](https://packages.debian.org/en/jessie/apt-clone).
