---
layout: post
title: Feeding Kd +3 of 100
read_time: true  
comments: true
category: Debugging
tags: [ WinDbg ]
---

* Show the bug check code and its parameters: `.bugcheck`.
* Show content of entries in the I/O system's error log: `!errlog`.
* Create a quick preliminary report: `!analyze -v;r;kv;lmnt;q`.

One line, each week.
