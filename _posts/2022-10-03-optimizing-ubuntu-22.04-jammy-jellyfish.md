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
Keep in mind that, as everything in life, nothing comes for free. Every optimization has its own pricetag and you must decide how much you are willing to pay for it.

### Swap space
When working with less than 16 Gb RAM, Ubuntu tends to do a lot of swapping. This leads to a lot of write actions to your SSD which in their turn slow down your system and chip away chunks of disk total lifetime.
Swap_tendency can be set to 0 (off) or 100 (on full-time). The standard Ubuntu setting is not optimal at the least (more info [here](https://rudd-o.com/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that) and needs some adjusting.

