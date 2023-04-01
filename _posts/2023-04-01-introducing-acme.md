---
layout: post
title: Introducing Acme, the Bell Labs Text Editor
read_time: true  
comments: true
category: Open Source
tags: [ Linux Tutorials, Developer Tools ]
---

Since I was talking about editors, next to Vim, Acme is on of my favs too. Nothing but yellow windows and blue bars on the screen, written by Rob Pike for Plan 9 in the early 1990s.

Acme is a program that combines aspects of window systems, shells, and editors to address common issues in the context of textual applications. It is
designed to support software development, but falls short of being a true programming environment. It is not a ‘toolkit’; it is a self-contained program, more like a shell than a library, that joins users and applications. 

From the perspective of the application (compiler, browser, etc.), it provides a universal communication mechanism, based on familiar Unix® file operations, that permits small applications even shell procedures to exploit the graphical user interface of the system and communicate with each other. For the user, the interface is extremely spare, consisting only of text, scroll bars, one simple kind of window, and a unique function for each mouse button no widgets, no icons, not even pop-up menus. Despite these limitations, acme is an effective environment in which to work and, particularly, to program.

It's difficult to explain acme without seeing it, though, so I've added a screencast from [Russ Cox](https://www.youtube.com/watch?v=dP1xVpMPn8M) explaining the basics of acme and showing a brief programming session. Remember as you watch the video that the 854x480 screen is quite cramped. Usually you'd run acme on a larger screen: even my MacBook Air has almost four times as much screen real estate. 

[![Watch the video](https://youtu.be/dP1xVpMPn8M)
