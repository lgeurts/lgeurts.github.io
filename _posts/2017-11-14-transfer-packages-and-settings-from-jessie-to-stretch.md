---
layout: post
title: How to transfer your packages & settings from Jessie to the all new Strech
read_time: true  
comments: true
category: Open Source
tags: [  ] 
---

1. List the currently installed packages, save them to a file 'my-settings' and then read that file to reinstall:

- $ dpkg -l | grep ^ii | awk '{print $2}' > my-settings

2. In your newly installed Debian-based distro, install the saved packages:

- $ sudo apt-get my-settings $(cat installed)
