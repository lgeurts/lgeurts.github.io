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

> * 07/22/17 Initial setup.

Changes since the last version:

v1.1

> * 08/02/17 Reworked the layout.
> * 08/04/17 Adding info for nftables, screenfetch, iftop, ttyload.
> * 08/07/17 Adding info for Claws Mail and Mutt.

**2 Before you begin**
----------------------

Set aside at least half a day to complete the basics –after basic installation and update you'll be adding and configuring a ton of extra files.

**3 Bunsen install**
---------------------

Download the appropriate ISO (bl-Deuterium-i386_20170429.iso).

Do an install from [Live USB](https://www.bunsenlabs.org/installation.html). As soon its finished, and after reboot, you will see underneath screen asking you to update the system. Press 'Enter'.

When the updating is done the script will run a set of options for attaching the Debian repositories, some 3rd party multimedia plugins, printer support, Java, and adding packages for developers. 

Each of these options may be selected individually.

![BunsenLabs Welcome](/assets/bunsenlabs-welcome.png)

**4 Productivity**
------------------

BunsenLabs contains a bunch of apps you can install with a simple click in the Openbox menu. 

Other apps are available from the repos & 3rd party sources. If so, instructions will show the appropriate commands (always run these as **sudo**). 

Let's start with the list.

**4.1 Internet browsers**

***• 4.1.1 Google Chrome, Firefox or Opera***

I made a choice for Firefox but you can install any browser next to it.

***Note:*** The plugins I'm presently using.

[Privacy Badger](https://www.eff.org/privacybadger), [HTTPS Everywhere](https://www.eff.org/https-everywhere), [Self-Destructing Cookies](https://addons.mozilla.org/en-US/firefox/addon/self-destructing-cookies/) & [DuckDuckGo Plus](https://addons.mozilla.org/en-US/firefox/addon/duckduckgo-for-firefox/).

**4.2 PDF reader**

***• 4.2.1 Evince***

Click and go.

**4.3 Office**

***• 4.3.1 LibreOffice***

LibreOffice Writer is the only software that comes preinstalled. However, the remainder of the suite is just a mouse click away.

***Note:*** I don't like the splash screen when starting LibreOffice. To get rid of it:

- $ geany /etc/libreoffice/sofficerc

Change Logo=1 to Logo=0 and exit.

***• 4.3.2 Claws Mail***

- $ apt-get install claws-mail

Claws Mail has an excellent [FAQ](http://www.claws-mail.org/faq/index.php/Main_Page) which covers virtually all your questions.
 
***Note:*** If you want to send and receive mail via a terminal, Mutt (patched) is a must.

- $ apt-get install mutt # the mail user agent.

- $ apt-get install mutt-patched # add sidebar, nntp support, multiple-fcc patches

For a copy of my .muttrc file, see the [BunsenLabs-Setup](https://github.com/lgeurts/BunsenLabs-Setup) repo. For everything else, [Mutt Wiki](https://dev.mutt.org/trac/wiki/MuttGuide).

**4.4 Graphics**

***• 4.4.1 Gimp***

***• 4.4.2 Viewnior***

Click, install.

**4.5 Multimedia apps**

***• 4.5.1 Mpd***

***• 4.5.2 Mpc***

***• 4.5.3 Ncmpcpp***

***• 4.5.4 YouTube-dl***

**5 Databases**
---------------

***• 5.1.1 PostgreSQL***

***• 5.1.2 PgAdmin***

**6 Development**
-----------------

My favs for simple coding and web site development. 

**6.1 Text Editors**

***• 6.1.1 Vim***

- $ apt-get install vim

 \*6.1.1.1 Bundle\*

 \*6.1.1.2 Pathogen\*

Pathogen is a Vim package manager that makes your life easier when working with Vim: it’s how you can have your fuzzy finders, file trees, and coding tools without drowning in Vimscript. 

I prefer Pathogen to some of the alternate Vim package managers because it's arguably the most popular (every plugin these days supporting it) and it's zero -config: just drop Vim plugins into the ~/.vim/bundle folder, and it’s installed. From there you can configure your ~/.vimrc file to taste.

- $ apt-get install vim-pathogen

 \*6.1.1.3 Tmux\*

- $ apt-get install tmux

***• 6.1.2 Gvim***

- $ apt-get install gvim

***• 6.1.3 Sublime 3***

**6.2 Programming**

***• 6.2.1 Python***

***• 6.2.2 Ruby***

**6.3 Frameworks**

***• 6.3.1 Rails***

**6.4 Static Web Generators**

***• 6.4.1 Jekyll***

**6.5 Version Control Systems**

***• 6.5.1 Git***

**7 Security**
--------------

**7.1 Firewall**

***• 7.1.1 Nftables***

- $ apt-get install -t jessie-backports nftables
- $ cd /usr/share/doc/nftables/examples/syntax/
- $ cp workstation /etc/nftables.conf 
- $ sed -i 's/flush/#flush/' /etc/nftables.conf 
- $ systemctl start nftables
- $ systemctl enable nftables
- $ nft list ruleset # check if rules have been applied after boot
- $ systemctl status nftables.service # check if .service has been started 

***Note:*** You now have a "whitelist" firewall that only accepts connections you created yourself. 
Problems? [Follow this thread on the BunsenLabs forums](https://forums.bunsenlabs.org/viewtopic.php?id=1765).

Use this basic firewall in addition to restrictive rules on your router!

**7.2 Mail encryption**

***• 7.2.1 GPG/PGP***

**8 System information**
------------------------

**8.1 Bash Scripts**

***• 8.1.1 Screenfetch***

Screenfetch displays system information alongside the ASCII version of the Linux distribution Logo of the system.

- $ apt-get install screenfetch

***Note:*** Instead Screenfetch you can install [Neofetch](https://github.com/dylanaraps/neofetch/wiki/Neofetch-vs-Screenfetch).

**8.2 System Monitors**

***• 8.2.1 iftop***

- $ apt-get install iftop

***• 8.2.2 ttyload***

- $ apt-get install ttyload

**9 Theming your Openbox desktop**
----------------------------------
Some eye candy because not everything is just about functionality, right?
