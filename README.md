# Chromebook-Crouton-Ubuntu-18.04-LAMP-WP
Ubuntu 18.04 based LAMP stack for crouton with optional WordPress target.
Created from a need to have a development environment on a chromebook with ARM processor, but should work anywhere crouton does.

### Open terminal and enter shell.

Press `Ctrl+Alt+T` to enter terminal.

Type `shell` hit enter.

### Download crouton and install to /usr/local/bin

`sudo mkdir /usr/local/bin`

`sudo curl -L -# -o /usr/local/bin/crouton https://github.com/dnschneid/crouton/raw/master/installer/crouton && sudo chmod +x /usr/local/bin/crouton`

### Download and save Ubuntu 18.04 release name BIONIC and create a bootstrap to save time on reinstalls.

`sudo crouton -r bionic -d -f ~/Downloads/mybootstrap.tar.bz2`

### Install enough targets to boot.

`sudo crouton -f ~/Downloads/mybootstrap.tar.bz2 -t core,audio,cli-extra`
#### Enter Crouton.
`sudo enter-chroot -n bionic`

*When prompted create a username and password.*

#### Install some basic software while in crouton and exit.
`sudo apt install xterm xinit`

#### Install additional targets.
`sudo crouton -n bionic -t xiwi,extension,keyboard -u`

#### Install LAMP target.

`sudo crouton -n bionic -T ~/Downloads/lamp -u`

#### Install WordPress target.
`sudo crouton -n bionic -T ~/Downloads/wp -u`

### Autostart Crouton when Chromebook starts by copying these files into ChromeOS.

`sudo cp ~/Downloads/crouton.conf /etc/init/`

`sudo cp ~/Downloads/crouton.init /usr/local/`

### Backup

`sudo edit-chroot -b bionic -f ~/Downloads/`

### Restore
`sudo edit-chroot -f ~/Downloads/ -r bionic`


