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

### Swap space (dismiss when having more than 16 Gb RAM)
When working with less than 16 Gb RAM, Ubuntu tends to do a lot of aggresive swapping. This leads to a lot of write actions to your SSD which in their turn slow down your system and chip away chunks of disk total lifetime.
The standard Ubuntu swap_[tendency setting](https://unix.stackexchange.com/questions/134202/when-is-swap-triggered-or-how-to-calculate-swap-tendency#134206) is not optimal (more info [here](https://rudd-o.com/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that)) and needs some adjusting.

