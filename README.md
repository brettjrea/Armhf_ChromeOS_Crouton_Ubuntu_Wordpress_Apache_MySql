# Crouton-LAMP/WP
Ubuntu 18.04 based LAMP stack for crouton with optional WordPress.

On Chromebook.

Open a shell (Ctrl+Alt+T, type "shell" no quotes and hit enter).
_______________________________________________________
###Download crouton and install to bin
_______________________________________________________
sudo mkdir /usr/local/bin

sudo curl -L -# -o /usr/local/bin/crouton https://github.com/dnschneid/crouton/raw/master/installer/crouton && sudo chmod +x /usr/local/bin/crouton
_______________________________________________________
###Download Ubuntu 18.04 release name BIONIC and create a bootstrap to save time.
_______________________________________________________
sudo crouton -r bionic -d -f ~/Downloads/mybootstrap.tar.bz2 (dl bootstrap)
-------------------------------------------------------
###Autostart Crouton when Chromebook starts###
------------------------------------------------------
sudo cp ~/Downloads/crouton.conf /etc/init/

sudo cp ~/Downloads/crouton.init /usr/local/
-------------------------------------------------------
###Install common base targets, create user and password install needed software, install additional base targets.
_______________________________________________________

sudo crouton -f ~/Downloads/mybootstrap.tar.bz2 -t core,audio,cli-extra

sudo enter-chroot -n bionic

sudo apt install xterm xinit g++

sudo crouton -n bionic -t xiwi,extension,keyboard -u
-------------------------------------------------------
###Install LAMP target and optional WP target.
_______________________________________________________
sudo crouton -n bionic -T ~/Downloads/lamp -u

sudo crouton -n bionic -T ~/Downloads/wp -u
_______________________________________________________
###Backup & Restore
-------------------------------------------------------

sudo edit-chroot -b bionic -f ~/Downloads/ (backup)

sudo edit-chroot -f ~/Downloads/ -r bionic
(restore)

--------------------------------------------------------


