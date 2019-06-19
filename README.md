# Chromebook-Crouton-Ubuntu 18.04-LAMP-WP
Ubuntu 18.04 based LAMP stack for crouton with optional WordPress target.
Created from a need to have a development environment on a chromebook with arm processor.

## Open terminal and enter shell.

On Chromebook.

Press Ctrl+Alt+T to enter terminal.
Type "shell" without the quotes and hit enter.

## Download crouton and install to bin

sudo mkdir /usr/local/bin

sudo curl -L -# -o /usr/local/bin/crouton https://github.com/dnschneid/crouton/raw/master/installer/crouton && sudo chmod +x /usr/local/bin/crouton

## Download Ubuntu 18.04 release name BIONIC and create a bootstrap to save time.

sudo crouton -r bionic -d -f ~/Downloads/mybootstrap.tar.bz2 (dl bootstrap)

## Autostart Crouton when Chromebook starts

sudo cp ~/Downloads/crouton.conf /etc/init/

sudo cp ~/Downloads/crouton.init /usr/local/

## Install enough system to create a user and password, and install some needed software, install additional needed targets.

sudo crouton -f ~/Downloads/mybootstrap.tar.bz2 -t core,audio,cli-extra

sudo enter-chroot -n bionic

sudo apt install xterm xinit g++

sudo crouton -n bionic -t xiwi,extension,keyboard -u

## Install LAMP target and optional WP target.

sudo crouton -n bionic -T ~/Downloads/lamp -u

sudo crouton -n bionic -T ~/Downloads/wp -u

## Backup & Restore

sudo edit-chroot -b bionic -f ~/Downloads/ (backup)

sudo edit-chroot -f ~/Downloads/ -r bionic
(restore)


