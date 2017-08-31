---
layout: post
title: My BunsenLabs Linux setup notes for Dell Inspiron 6000
read_time: true  
comments: true
category: Open Source
tags: [ Operating Systems, Tutorials ]
---

![BunsenLabs Deuterium, fresh install](/assets/bunsenlabs-deuterium.jpg)

I was a **#!** user until it's main developer, [Phillip Newborough](https://corenominal.org), ended the project after releasing CrunchBang 11 in May 6, 2013. Looking for something similar, I found and installed the BunsenLabs [Hydrogen](http://distrowatch.com/table.php?distribution=bunsenlabs) distro. 

BunsenLabs does not use a traditional desktop like KDE, GNOME or even Xfce. Instead it's an optimized mix of components from various open source projects including most notably the lightweight Openbox window manager, tint2 panel, the Conky system monitor, and Thunar file manager.

The guide is based on [Deuterium](https://www.bunsenlabs.org/installation.html#downloads) which serves as my main coding OS. It offers a speedy, uncluttered Debian experience which (in my opinion) is only equaled by distros as for example [ArchLabs Linux](https://archlabsblog.wordpress.com/) or [CrunchBang++](https://www.crunchbangplusplus.org/).

Here is a rundown of how I configured BunsenLabs to best serve my needs.

**1 Status of this document**
-----------------------------

v1.0
> * 07/11/17 Initial setup.

Changes since the last version:

v1.1
> * 08/02/17 Reworked the layout.
> * 08/04/17 Adding nftables, screenfetch, iftop, ttyload.
> * 08/05/17 Adding LibreOffice, Claws Mail, mutt, Krita.
> * 08/07/17 Adding PostgreSQL, pgAdmin.
> * 08/08/17 Adding mpd, ncmpcpp, curl, youtube-dl.
> * 08/10/17 Adding GnuPG, Sublime Text 3, Jekyll.
> * 08/13/17 Adding vim, Pathogen, Gvim, Python, pip.
> * 08/15/17 Adding Git, Node.js, Ruby on Rails, Tint2.
> * 08/17/17 Adding terminator.
> * 08/20/17 Made multiple adjustments, removed typos.
> * 08/29/17 Adding Geany-plugins, ranger, nicstat, lshw, dzen2.

**2 Before you begin**
----------------------

As a good practice, before installation I always first boot the system from Live USB or DVD and download/run [lshw](https://packages.debian.org/jessie/utils/lshw) to check the hardware components.

In rare cases when using a WiFi connection to connect to the internet, the Pro 2200BG adapter is not recognized during setup. Just ignore any system update. Same for anything related to Bunsen repositories; after install WiFi works fine, and you can add [the repos](https://forums.bunsenlabs.org/viewtopic.php?id=1526) manually in /etc/apt/sources.list.

**3 Bunsen install**
---------------------

Download the appropriate ISO (bl-Deuterium-i386_20170429.iso).

Do an install from [Live USB](https://www.bunsenlabs.org/installation.html). As soon its finished, and after reboot, you will see underneath screen asking you to update the system. Press 'Enter'.

When the updating is done the script will run a set of options for attaching the Debian repositories, some 3rd party multimedia plugins, printer support, Java, and adding packages for developers. 

Each of these options may be selected individually.

![BunsenLabs Welcome](/assets/bl-welcome.png)

**4 Productivity**
------------------

BunsenLabs contains a bunch of apps you can install with a simple click in the Openbox menu. 

Other apps are available from the repos & 3rd party sources. If so, instructions will show the appropriate commands (always run these as **non-root user** with [sudo](https://wiki.debian.org/sudo) privileges). 

Let's start with the list.

**4.1 Internet browsers**

***• 4.1.1 Google Chrome, Firefox or Opera***

I made a choice for Firefox but you can install any browser next to it.

***Note:*** The plugins I'm presently using.

[Privacy Badger](https://www.eff.org/privacybadger), [HTTPS Everywhere](https://www.eff.org/https-everywhere), [Self-Destructing Cookies](https://addons.mozilla.org/en-US/firefox/addon/self-destructing-cookies/), [Stylish](https://addons.mozilla.org/en-US/firefox/addon/stylish/) & [Duck DuckGo Plus](https://addons.mozilla.org/en-US/firefox/addon/duckduckgo-for-firefox/).

**4.2 Office**

***• 4.2.1 LibreOffice***

LibreOffice Writer is the only software that comes pre-installed. However, the remainder of the suite is just a mouse click away.

***Note:*** I don't like the splash screen when starting LibreOffice. To get rid of it:

- $ geany /etc/libreoffice/sofficerc

Change Logo=1 to Logo=0 and exit.

***• 4.2.2 Claws Mail***

- $ apt-get install claws-mail

Claws Mail has an excellent [FAQ](http://www.claws-mail.org/faq/index.php/Main_Page) which covers virtually all your questions.
 
***Note:*** If you want to send and receive mail via a terminal, Mutt (-patched) is a must.

![Mutt client](/assets/mutt.png)

- $ apt-get install mutt # the mail user agent
- $ apt-get install mutt-patched # adds sidebar, nntp support, multiple-fcc patches

For a copy of my dots, see [this](https://github.com/lgeurts/BunsenLabs-Setup/tree/master/.mutt) repo. For everything else, [Mutt Wiki](https://dev.mutt.org/trac/wiki/MuttGuide).

**4.3 Graphics**

***• 4.3.1 Gimp***

Obligatory. Just a click away.

***• 4.3.2 Viewnior***

I don't like the standard Mirage picture viewer.

***Note:*** I am not using this, but if you are looking for a professional open source painting program with full support for graphics tablets, check out [Krita](https://krita.org/en/).

**4.4 Multimedia apps**

***• 4.4.1 Mpd***

- $ apt-get install mpd

To configure mpd (Music Player Daemon), download [this script](https://github.com/ronalde/mpd-configure).

***• 4.4.2 Ncmpcpp***

Probably the best free ncurses mpd client available.

![ncmpcpp](/assets/ncmpcpp.png)

- $ apt-get install ncmpcpp

***• 4.4.3 YouTube-dl***

- $ apt-get install [curl](https://packages.debian.org/jessie/curl) # command-line tool for transferring data
- $ curl -L [https://yt-dl.org/downloads/latest/youtube-dl](https://yt-dl.org/downloads/latest/youtube-dl) -o /usr/local/bin/ youtube-dl
- $ chmod a+rx /usr/local/bin/youtube-dl

**5 Relational Databases**
--------------------------

***• 5.1.1 PostgreSQL***

- $ apt-get install postgresql-9.4 postgresql-client-9.4

Next, read this [How to install and use PostgreSQL 9.4 on Debian 8](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-9-4-on-debian-8) article. 

***• 5.1.2 pgAdmin***

pgAdmin is a graphical administration tool for PostgreSQL.

- $ apt-get install pgadmin3
 
There are forums which discuss a version 4 install on Jessie but I prefer stable, not the latest bleeding edge.

**6 Development**
-----------------

My favs for simple coding and web site development. 

**6.1 Text Editors**

***• 6.1.1 Vim***

- $ apt-get install vim

That's done. Now, we will version our configuration to share across machines while keeping track of any changes made.

To do this, create a .vim repository with a vimrc file:

- $ cd ~
- $ mkdir .vim
- $ cd .vim
- $ touch vimrc
- $ git init .

And [symlink](https://wiki.debian.org/SymLink) the vimrc file. This way we can (ab)use it while still getting all the advantages of versioning with Git.

- $ cd ~
- $ ln -s ~/.vim/vimrc ~/.vimrc

Next step is theming and changing the layout:

- $ mkdir ~/.vim/colors

Copy my [theme git files](https://github.com/lgeurts/BunsenLabs-Setup/tree/master/.vim/colors) to the colors folder. Edit .vimrc and add this line:

> * `colorscheme Tomorrow-Night`

Some syntax highlighting based on file names would be appreciated:

> * `filetype on`
> * `filetype plugin on`

And text formatting:

> * `filetype indent on`

Set default font to [Menlo](https://github.com/lgeurts/BunsenLabs-Setup/tree/master/.fonts) regular with a size 17:

> * `set guifont=Menlo\ Regular:h17`

While we are busy also add these lines:

> * `set lines=35 columns=150`
> * `set colorcolumn=90`
> * `set number`
> * `syntax on`

***Note:*** Now that your vim starts to look better, let’s improve how it functions. Either visit this [repo](https://github.com/amix/vimrc) for further customization (learn while doing), or copy my dotfile (see end of sub 6.1.1.2).

 \*6.1.1.1 Pathogen\*

Pathogen is a vim package manager that makes your life easier when working with vim: it’s how you can have your fuzzy finders, file trees, and coding tools without drowning in Vimscript. 

I prefer Pathogen to some of the alternate vim package managers because it's arguably the most popular (every plugin these days supporting it) and it's zero -config: just drop a vim plugin into the ~/.vim/bundle folder, and it’s installed. From there you can configure the ~/.vimrc file to your taste.

- $ mkdir -p ~/.vim/autoload ~/.vim/bundle && \
- $ curl -LSso ~/.vim/autoload/pathogen.vim [https://tpo.pe/pathogen.vim](https://tpo.pe/pathogen.vim)

Add this line to the top of your .vimrc:

> * `execute pathogen#infect()`

***Note:*** See [Romain Lafourcade's](https://github.com/romainl) gist '[How to use Tim Pope's Pathogen](https://gist.github.com/romainl/9970697)'.

\*6.1.1.2 Vim plugins\*

![vim](/assets/vim.png)

All plugins are on Git which makes updating to the latest version very easy, i.e. pulling master.

For every plugin you need to run:

- $ cd ~/.vim
- $ git submodule add git@source/pluginname.git bundle/pluginname

For example, adding the vim-ruby plugin:

- $ git submodule add git@github.com:vim-ruby/vim-ruby.git bundle/vim -ruby

Name          | Link
------------- | --------
Command-T     | [https://github.com/wincent/command-t/](https://github.com/wincent/command-t/)
NerdCommenter | [https://github.com/scrooloose/nerdcommenter](https://github.com/scrooloose/nerdcommenter)
NerdTree      | [https://github.com/scrooloose/nerdtree](https://github.com/scrooloose/nerdtree)
Lightline     | [https://github.com/itchyny/lightline.vim](https://github.com/itchyny/lightline.vim)
Supertab      | [https://github.com/ervandew/supertab](https://github.com/ervandew/supertab)
Fugitive      | [https://github.com/tpope/vim-fugitive](https://github.com/tpope/vim-fugitive)
Git Gutter    | [https://github.com/airblade/vim-gitgutter](https://github.com/airblade/vim-gitgutter)
Bundler       | [https://github.com/tpope/vim-bundler](https://github.com/tpope/vim-bundler)
Endwise       | [https://github.com/tpope/vim-endwise](https://github.com/tpope/vim-endwise)
Ruby          | [https://github.com/vim-ruby](https://github.com/vim-ruby)
Rails         | [https://github.com/tpope/vim-rails/](https://github.com/tpope/vim-rails/)
Dispatch      | [https://github.com/tpope/vim-dispatch](https://github.com/tpope/vim-dispatch)
Multiple Cursors | [https://github.com/terryma/vim-multiple-cursors/](https://github.com/terryma/vim-multiple-cursors/)

***Note:*** My [memo](/assets/vim-plugin-settings.txt) for activating Command-T, NerdTree and Git Gutter in .vimrc.             Feeling lazy? Download my latest [config](https://github.com/lgeurts/BunsenLabs-Setup/tree/master/.vim/).

***• 6.1.2 Gvim***

![Gvim Editor](/assets/gvim.png)

- $ apt-get install gvim

***• 6.1.3 Sublime Text 3***

- $ wget [http://bit.ly/2vTirOt](http://bit.ly/2vTirOt) # //c758482.r82.cf2.rackcdn.com/sublime-text_build-3083_i386.deb
- $ dpkg -i sublime-text_build-3083_i386.deb

***Note:*** [Sublime](https://www.sublimetext.com/) is non-free. If you are willing to pay some money, you'll get one slick source code editor.

**6.2 Programming**

***• 6.2.1 Python***

Jessie ships with both **Python 2** and **Python 3** pre-installed. Let’s update and upgrade the system:

- $ apt-get update
- $ apt-get -y upgrade 

Once the process is complete, we check the Python 3 version by typing:

- $ python3 -V
  * *Python 3.4.2*

Guess I'll add [pip](https://packages.debian.org/jessie/python3-pip), Always handy to have a package installer aboard:

- $ apt-get install -y python3-pip

We need a few more packages and development tools to ensure that we have a robust setup:

- $ apt-get install build-essential libssl-dev libffi-dev python-dev

Setting up isolated project spaces (virtual environment):

- $ cd ~
- $ apt-get install -y python3-venv
- $ mkdir py3venv
- $ cd py3venv

Creating a project directory:

- $ python3 -m venv 'projectname' 

Enable the project environment:

- $ source 'projectname'/bin/activate

Probably Jessie uses Python version 2.7 as system default:

- $ python -V
  * *Python 2.7.9*

I will use the update-alternatives command to set 3.4 as the new standard:

- $ update-alternatives --install /usr/bin/python python /usr/bin/python2.7
'1' # lowest number
- $ update-alternatives --install /usr/bin/python python /usr/bin/python3.4
'2' # higher number which will prevail

Checking if it worked: 

- $ python -V 
  * *Python 3.4.2*

Listing all Python alternatives:

- $ update-alternatives --list python 
  * */usr/bin/python2.7*
  * */usr/bin/python3.4*

From now on, typing:

- $ update-alternatives --config python

will make it possible to switch versions by entering a selection number. 

***• 6.2.2 Ruby on Rails***

Change dir to your home:

- $ cd ~    

Get the installation script:

- $ curl -sL [https://deb.nodesource.com/setup_6.x](https://deb.nodesource.com/setup_6.x) -o nodesource_setup.sh

Running the script in ~ (will take some time):

- $ bash nodesource_setup.sh

After running the setup script, install the Node.js package. 

- $ apt-get install nodejs

This nodejs binary package contains both nodejs and npm. In order for some of the npm packages to work:

- $ apt-get install build-essential

Use gpg to contact a key server and request the RVM project's key:

![RVM key](/assets/rvm-project-key.png)

***Note:*** 409B6B1796C275462A1703113804BB82D39DC0E3.

Download the RVM installation script:

 - $ curl -sSL https://get.rvm.io -o rvm.sh

Pipe the script to bash to install Rails and the associated latest release of Ruby:

![Piping RVM](/assets/rvm-pipe.png)

During the installation process, you'll be prompted for your password. Enter as requested and RVM gets all tools it needs to build and compile Ruby, download the latest version of Ruby, the Ruby on Rails framework, and its dependencies.

When the installation is complete, source the RVM scripts:

- $ source ~/.rvm/scripts/rvm

A final check that Ruby is correctly installed:

- $ which ruby

***Note:*** Robby Russell wrote a [script](https://github.com/robbyrussell/laptop) that transforms your Jessie laptop in a Rails development machine. Use at your own risk.

**6.3 Version Control System**

***• 6.3.1 Git***

- $ apt-get install git-core
- $ git config --global user.name 'username'
- $ git config --global user.email 'username@example.com'
- $ git config --list # verify settings

**6.4 Static Site Generator**

***• 6.4.1 Jekyll***

For installation and setting up a GitHub Pages site locally with Jekyll click [here](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/).

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

***Note:*** You now have a "whitelisted" firewall that only accepts connections you created yourself. 
Problems? [Follow this thread on the BunsenLabs forums](https://forums.bunsenlabs.org/viewtopic.php?id=1765).

Use this basic firewall in addition to restrictive rules on your router!

**7.2 Mail encryption**

***• 7.2.1 GnuPG/GPG***

Full setup notes for creating your private and public keys on [NixCraft](https://www.cyberciti.biz/tips/linux-how-to-create-our-own-gnupg-privatepublic-key.html). Mutt and GnuPG? See Justin R. Miller's [tutorial](http://codesorcery.net/old/mutt/mutt-gnupg-howto).

**8 System information**
------------------------

**8.1 Bash Scripts**

***• 8.1.1 Screenfetch***

Displays system information and ASCII version of the Linux distro logo.

- $ apt-get install screenfetch

***Note:*** Instead Screenfetch you can install [Neofetch](https://github.com/dylanaraps/neofetch/wiki/Neofetch-vs-Screenfetch).

**8.2 System Monitors**

***• 8.2.1 iftop***

Tool that produces a frequently updated list of network connections.

![iftop](/assets/iftop.png)

- $ apt-get install iftop

***• 8.2.2 ttyload***

Tracks load averages over time on a UNIX(ish) machine.

![ttyload](/assets/ttyload.png)

- $ apt-get install ttyload

**9 Theming your Openbox desktop**
----------------------------------

Some eye candy because not everything is just about functionality, right?

**9.1 Terminal Colors**

***• 9.1.1 Terminator***

Copy the config from [here](https://github.com/lgeurts/BunsenLabs-Setup/tree/master/.config/terminator) and replace the default file in ~/.config/terminator. 

![terminator](/assets/terminator-colors.png)

***Note:*** If you want to design your own scheme, visit [terminal.sexy](https://terminal.sexy/).

**9.2 System Panel/Taskbar**

***• 9.2.1 Tint2***

Tint2 features:

- Comes with Openbox.
- Panel with taskbar, systray, clock and battery status.
- Customize color/transparency on font, icon, border and background.
- Pager like capability: send task from one workspace to another, switching workspaces.
- Multi-monitor: one panel per monitor, show tasks from current monitor.
- Customize mouse events.
- Window manager's menu.

Download [oomox-colors.tint2rc](https://github.com/lgeurts/BunsenLabs-Setup/tree/master/.config/tint2) and drop it in ~/.config/tint2.

**9.3 Window Manager**

***• 9.3.1 Openbox***

Fonts, icons, customize rc.xml & autostart > window decorations & disable conky.

**9.4 Internet Browser**

***•9.4.1 Firefox*** 

![Firefox Web Browser](/assets/firefox.png)

Download this homepage for Firefox [here](https://github.com/unix121/homepage).

**10 Extras**
-------------

Packages I use on a daily basis but often forget to install in a new setup:

- $ apt-get install [geany-plugins](https://packages.debian.org/jessie/geany-plugins) [ranger](https://packages.debian.org/jessie/utils/ranger) [nicstat](https://packages.debian.org/jessie/nicstat) [dzen2](https://packages.debian.org/jessie/x11/dzen2)

**YOU ARE DONE**

