---
layout: post
title: My BunsenLabs Linux setup notes for Dell Inspiron 6000
read_time: true  
comments: true
category: Open Source
tags: [ Linux, Tutorials ]
---

![BunsenLabs Deuterium, fresh install](/assets/bunsenlabs-deuterium.jpg)
I was a **#!** user until it's main developer, [Phillip Newborough](https://corenominal.org), ended the project after releasing CrunchBang 11 (Waldorf) in May 6, 2013. Looking for something similar, I found and installed the BunsenLabs [Hydrogen](http://distrowatch.com/table.php?distribution=bunsenlabs) distro. 

BunsenLabs does not use a traditional desktop like a KDE, GNOME or even Xfce. Instead it's an optimized mix of components from various open source projects including most notably the lightweight Openbox window manager, tint2 panel, the Conky system monitor, and Thunar file manager.

This guide is based on [Deuterium](https://www.bunsenlabs.org/installation.html#downloads) which serves as my main OS. Overall, it offers a speedy, uncluttered Debian experience which (in my opinion) is only equaled by distros as for example [ArchLabs Linux](https://archlabsblog.wordpress.com/) or [CrunchBang++](https://www.crunchbangplusplus.org/).

Here is a rundown of how I configured BunsenLabs to best serve my needs.

**1 Status of this document**
-----------------------------

v1.0

> Changes since the last version:

> •

**2 Before you begin**
----------------------

Set aside at least half a day to complete the basics –after basic installation and update you'll be adding and configuring a ton of extra files.

**3 Bunsen install**
---------------------

Download the appropriate ISO (for JARREAU bl-Deuterium-i386_20170429.iso).

Do an install from [Live USB](https://www.bunsenlabs.org/installation.html). As soon its finished, and after reboot, you will see underneath screen asking you to update the system. Press 'Enter'.

When the updating is done the script will run a set of options for attaching the Debian repositories, some 3rd party multimedia plugins, printer support, Java, and adding packages for developers. 

Each of these options may be selected individually.

![BunsenLabs Welcome](/assets/bunsenlabs-welcome.png)

**4 Desktop apps**
------------------

BunsenLabs contains a bunch of apps you can install via the Openbox menu. Let's run thru the list.

**4.1 Internet browser**

You have a choice between Google Chrome, Firefox and Opera (I opted for FF).

***Note:*** the list of plugins I'm presently using:

[Privacy Badger](https://www.eff.org/privacybadger), [HTTPS Everywhere](https://www.eff.org/https-everywhere), [Self-Destructing Cookies](https://addons.mozilla.org/en-US/firefox/addon/self-destructing-cookies/) & [DuckDuckGo Plus](https://addons.mozilla.org/en-US/firefox/addon/duckduckgo-for-firefox/).

**4.2 PDF reader**

Click and go.

**4.3 LibreOffice**

LibreOffice Writer is the only software that comes preinstalled. However, the remainder of the suite is just a mouse click away.

***Note:*** I don't like the splash screen when starting LibreOffice. To get rid of it, 

**4.4**

**4.5**

**5 Additional tools**
----------------------

Some of these are from the repositories, some fom oher sources. 

**5.1 Multimedia**

• **5.1.1 YouTube-dl**

• **5.1.2 Ncmpcpp**

**5.2 Development**

• **5.2.1 Git**

• **5.2.2 Ruby and Rails**

• **5.2.3 Jekyll**

• **5.2.4 Sublime Text Editor**

**5.3 Security**

• **5.3.1 GPG/PGP**
