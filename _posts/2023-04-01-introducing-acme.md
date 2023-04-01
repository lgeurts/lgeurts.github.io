---
layout: post
title: Introducing Acme, the Bell Labs Text Editor
read_time: true  
comments: true
category: Open Source
tags: [ Linux Tutorials, Developer Tools ]
---

Since I was talking about Vim, the Acme Text Editor written by [Rob Pike](https://github.com/robpike) for [Plan 9](https://p9f.org/) in the early 1990s is another favorite. Nothing but yellowish windows and blue bars on the screen, no fuzz.

Acme combines several aspects of window systems, shells, and editors. Designed to support software development but not a true programming toolkit. Instead, it is a self-contained program; more like a shell than a library, that joins users and applications. 

From the perspective of the application e.g. compiler, browser, etc., it provides a universal communication mechanism based on familiar Unix or GNU - Linux file operations, that permits your small applications even shell procedures to exploit the graphical user interface of the system and communicate with each other.  
For the user, the interface is extremely spare, consisting only of text, scroll bars, one simple kind of window, and a unique function for each mouse button. There are no widgets, no icons, not even pop-up menus.  
Despite these GUI limitations, Acme is still an effective environment in which to work and, particularly, to program.

It's rather difficult to explain how it works without seeing it though, so I added a screencast from [Russ Cox's Golang page](https://www.youtube.com/@rscgolang) showing a brief programming session. 

[![Watch the video](/assets/acme-editor.png)](https://youtu.be/dP1xVpMPn8M)

***PS. Each time people tell me today's Acme users are borderline insane, I send them the above link and they quickly change their mind.***
