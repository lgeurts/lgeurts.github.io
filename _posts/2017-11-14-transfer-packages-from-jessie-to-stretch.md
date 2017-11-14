---
layout: post
title: How to transfer your package list from Jessie to the all new Strech
read_time: true  
comments: true
category: Open Source
tags: [  ] 
---

List the currently installed packages, save them to a file 'my-packages' and then read that file to re-install:

```$ dpkg -l | grep ^ii | awk '{print $2}' > my-packages```

In your newly installed Debian-based distro, install the saved packages:

```$ sudo apt-get install $(cat my-packages)```
