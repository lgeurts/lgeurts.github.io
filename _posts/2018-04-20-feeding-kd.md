---
layout: post
title: Feeding Kd +3 of 100
read_time: true  
comments: true
category: Debugging
tags: [ WinDbg ]
---

1. Show the bug check code and its parameters: `.bugcheck`.
2. Show the content of any pending entries in the I/O system's error log: `!errlog`.
3. Create a quick preliminary report: `!analyze -v;r;kv;lmnt;q`.

One line, each week.
