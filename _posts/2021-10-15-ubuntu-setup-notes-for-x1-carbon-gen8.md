---
layout: post
title: To-do's when (re)installing Ubuntu desktop on a Lenovo ThinkPad X1 Carbon Gen 8
read_time: true
comments: true
category: Open Source 
tags: [ Linux Tutorials ]
---

<img src="/assets/groovy-gorilla.png" width="654">

# BIOS functions

## Firmware updates

Lenovo sends out capsules which when running Ubuntu Update-Manager will be available for installation. Ref: [Lenovo Knowledge Base](https://support.lenovo.com/nl/en/solutions/ht510810-how-to-do-software-updates-linux).

## Sleep states

The BIOS has 2 Sleep State options, which you can find in Config > Power > Sleep State. 

The Linux option is a **traditional S3** power state where all hardware components are turned off except for the RAM, and it should work normally. 

The Windows option is a **newer software-based** "modern standby" which works on Linux (despite the name). One **benefit** to the **Windows** sleep state is **a faster wake up time**, a possible **drawback** is **increased power usage**. 

<p align="center">
    Tested the Windows option > did not notice any major loss on battery time.
</p>

# Software packages

## My bash & zsh history output
```
$ sudo apt install ubuntu-restricted-extras
$ sudo apt install tmux
$ sudo apt install neofetch
$ sudo apt install curl
$ sudo apt install youtube-dl
$ sudo apt install gimp
$ sudo apt install vim
$ sudo apt install python
$ sudo apt install git
$ sudo apt install htop
$ sudo apt install iotop
$ sudo apt install iftop
$ sudo apt install ttyload
$ sudo apt install ranger
$ sudo apt install unrar zip unzip p7zip-full p7zip-rar rar
$ sudo apt install virtualbox virtualbox-ext-pack -y
 <> $ sudo sh sign-vboxmodules.sh
$ sudo apt install steam
$ sudo apt install spotify
$ sudo add-apt-repository ppa:yann1ck/onedrive
 <> $ sudo apt update
 <> $ sudo apt install onedrive
 <> $ onedrive --synchronize --verbose --dry-run
 <> $ systemctl --user enable onedrive
 <> $ systemctl --user start onedrive
 <> $ systemctl status --user onedrive
$ sudo add-apt-repository -y ppa:teejee2008/ppa
 <> $ sudo apt update
 <> $ sudo apt install timeshift
$ curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
$ git clone https://github.com/powerline/fonts.git --depth=1
 <> $ cd fonts
 <> $ ./install.sh
 <> $ cd..
 <> $ rm -rf fonts
$ sudo apt update && sudo apt install ecryptfs-utils cryptsetup
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
 <> $ unzip awscliv2.zip
 <> $ sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin
 <> $ aws configure --profile **my username**
$ sudo apt install zsh
 <> $ zsh --version
 <> $ echo $SHELL
 <> $ chsh -s $(which zsh)
$ git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
$ git clone https://gitlab.gnome.org/GNOME/sushi.git
 <> $ cd sushi-3.38.0 (could be a newer version)
 <> $ sudo apt install meson libevince-dev gir1.2-gstreamer-1.0 librust-gstreamer-audio-sys-dev librust-gstreamer-audio-sys-dev libgtksourceview-4-dev libmusicbrainz5-dev libwebkit2gtk-4.0-dev libgirepository1.0-dev ninja-build
 <> $ meson builddir && cd builddir
 <> $ sudo meson install
$ sudo apt install gufw
$ sudo apt install mupdf
$ sudo apt -y install net-tools
$ sudo apt install smartmontools
$ sudo apt remove --purge totem
$ sudo apt update && sudo apt upgrade
$ sudo apt install mpv
$ sudo apt install ffmpeg
$ sudo apt install ffmpegthumbnailer
$ sudo apt install protonvpn
$ sudo apt install gnome-tweak-tool
$ sudo apt install gnome-shell-extensions
$ sudo apt install gnome-shell-extension-appindicator gir1.2-appindicator3-0.1
$ sudo apt install gnome-shell-pomodoro
$ sudo add-apt-repository -y ppa:libreoffice/ppa
 <> $ sudo apt update && sudo apt install libreoffice
$ sudo snap install hexchat
$ sudo snap install slack --classic
$ sudo snap install powershell --classic
$ sudo wget https://github.com/shiftkey/desktop/releases/download/release-2.6.3-linux1/GitHubDesktop-linux-2.6.3-linux1.deb
 <> $ sudo apt install gdebi-core
 <> $ sudo gdebi GitHubDesktop-linux-2.6.3-linux1.deb
$ sudo curl -O https://releases.hashicorp.com/vagrant/2.2.9/vagrant_2.2.9_x86_64.deb
 <> $ sudo apt install ./vagrant_2.2.9_x86_64.deb
$ sudo apt install flatpak gnome-software-plugin-flatpak gnome-software
$ flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
$ sudo flatpak install flathub io.atom.Atom
 <> $ flatpak run io.atom.Atom
$ apm install pigments
$ apm install file-icons
$ apm install teletype
$ apm install atom-beautify
$ apm install todo-show
$ apm install expose
$ apm install emmet
$ apm install color-picker
$ apm install markdown-writer
$ apm install language-markdown
$ apm install language-powershell
$ apm install autocomplete-python
$ apm install language-batchfile
$ apm install language-vbscript
$ apm install language-reg
$ apm install minimap
$ apm install minimap-autohider
$ apm install autoclose-html-plus
$ apm install text-align
$ cd "My Documents"
 <> $ find . -type f -print0 | xargs -0 chmod -x
$ gsettings set org.gnome.desktop.privacy remember-recent-files false
$ gsettings set org.gnome.settings-daemon.plugins.media-keys max-screencast-length 0
```
Resources: 
- [VirtualBox + Secure Boot + Ubuntu = fail](https://stegard.net/2016/10/virtualbox-secure-boot-ubuntu-fail/)
- [vim-plug: Vim plugin manager](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim)
- [Install Zsh, Oh-My-Zsh, Fonts-Powerline & Plugins (Ubuntu 18.04+)](https://gist.github.com/willianfalbo/a6a69de0ef83815174042363313ec668)
- [How to Use TimeShift to Backup and Restore Ubuntu Linux](https://github.com/teejee2008/timeshift) 
- [onedrive-abraunegg, free OneDrive Client for Linux](https://github.com/abraunegg/onedrive)
- [Thunderbird and Hotmail](https://support.mozilla.org/en-US/kb/thunderbird-and-hotmail)

**Note:** dotfiles are available in [this private repo](https://github.com/lgeurts/ubuntu-20.x-dotfiles).

## Browser extensions

Add [DuckDuckGo](https://addons.mozilla.org/en-US/firefox/addon/duckduckgo-for-firefox/), [Privacy Badger](https://privacybadger.org/), [HTTPS Everywhere](https://www.eff.org/https-everywhere), and [Facebook Container](https://github.com/mozilla/contain-facebook). Do not use other sources!

# System specifics

## Hibernation modus aka deep sleep

Simply closing the lid will probably trigger deep sleep. Check that it works using the command line:
```
$ systemctl suspend -i
```
If not, upgrade to a newer kernel.

## Low cTDP and trip temperature in Linux

This problem is related to 'thermal throttling' on Linux, which is set much below Windows values. It will cause your laptop to run slower than it could when under heavy stress.

Before attempting to apply this solution, make sure that the problem still exists. To do so, open a Linux terminal and run following commands:
```
$ sudo apt install msr-tools
$ sudo rdmsr -f 29:24 -d 0x1a2
```
If you see 3 as a result value (15 when running on the battery), you don’t have to do anything. Otherwise:

***Warning** - The next steps can cause serious issues on your system. See [this page](https://github.com/erpalma/throttled) for more details.*

1. Disable Secure Boot in the BIOS (won’t work otherwise).
2. Install the throttled fix:
```
$ sudo apt install git build-essential python3-dev libdbus-glib-1-dev libgirepository1.0-dev libcairo2-dev python3-cairo-dev python3-venv python3-wheel
$ git clone https://github.com/erpalma/throttled.git
 <> $ sudo ./throttled/install.sh
```
3. Make sure that thermald is not setting it back down:
```
$ sudo systemctl stop thermald.service
$ sudo systemctl disable thermald.service
```
4. If you want thermald permanently disabled, even after a package update:
```
$ sudo systemctl mask thermald.service
```
5. Verify that throttled is running:
```
$ sudo systemctl status throttled
```
6. Check again that the result from running the rdmsr command is 3.

## Battery temperature levels

I use lower temperature levels to preserve battery life at the cost of performance. To change default values, edit your /etc/throttled.conf file, and set Trip_Temp_C for both battery and AC the way you want:
```
[BATTERY]
# Other options here...
PL2_Tdp_W: 40
Trip_Temp_C: 75

[AC]
# Other options here...
PL1_Tdp_W: 34
PL2_Tdp_W: 40
Trip_Temp_C: 90
```

## Battery charging thresholds

There are a lot of theories and advisories about ThinkPad charging thresholds. 
Some say thresholds are needed to keep the battery healthy, some think they are useless and the battery will work the same just as it is.

I always stick with the following settings for my laptops (because they are mostly on AC):
```
Start threshold: 60% - Stop threshold: 65%
```
This means that charging will start only if the battery level goes down below 60% and will stop at 65%. This prevents my battery from being charged too often, and from being charged beyond a recommended level.

To achieve this for Linux based machines:
1. Install this list of packages:
```
$ sudo apt install tlp tlp-rdw acpi-call-dkms tp-smapi-dkms acpi-call-dkms
```
2. After that edit the /etc/tlp file and change below values:
```
# Uncomment both of them if commented out
START_CHARGE_THRESH_BAT0=60
STOP_CHARGE_THRESH_BAT0=65
```
3. Reboot, run:
```
$ sudo tlp-stat | grep tpacpi-bat
```
4. Verify that the values are as you expected:
```
tpacpi-bat.BAT0.startThreshold          = 60 [%]
tpacpi-bat.BAT0.stopThreshold           = 65 [%]
```
5. You can change these thresholds anytime, and apply changes typing:
```
$ sudo tlp start
```

**Note:** if you need your laptop fully charged, you can achieve that by running the following command while connected to AC:
```
$ tlp fullcharge
```
