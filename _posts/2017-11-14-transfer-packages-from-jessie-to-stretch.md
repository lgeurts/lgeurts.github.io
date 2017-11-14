---
layout: post
title: How to transfer a package list from Jessie to Stretch
read_time: true  
comments: true
category: Open Source
tags: [ Debian Linux ] 
---

```$ dpkg -l | grep ^ii | awk '{print $2}' > my-packages```

```$ sudo apt-get install $(cat my-packages)```

Or get [apt-clone](https://packages.debian.org/en/jessie/apt-clone).
