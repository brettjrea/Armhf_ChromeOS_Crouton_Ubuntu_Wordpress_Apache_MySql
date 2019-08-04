## Chromebook-Crouton-Ubuntu-18.04-LAMP
Instructions and files for an Ubuntu 18.04 based LAMP stack for [crouton](https://github.com/dnschneid/crouton).
Created from a desire to have a development environment on a chromebook with an ARM processor, but should work anywhere crouton does.

### The following instructions are written and depend on the repositories files being found in the ~/Downloads folder.

#### Open terminal and enter shell.

Press `Ctrl+Alt+T` to enter terminal.

Type `shell` hit enter.

#### Download crouton and install to /usr/local/bin

`sudo mkdir /usr/local/bin`

`sudo curl -L -# -o /usr/local/bin/crouton https://github.com/dnschneid/crouton/raw/master/installer/crouton && sudo chmod +x /usr/local/bin/crouton`

#### Download and save Ubuntu 18.04 release name BIONIC and create a bootstrap to save time on reinstalls.

`sudo crouton -r bionic -d -f ~/Downloads/mybootstrap.tar.bz2`

#### Install enough targets to boot.

`sudo crouton -f ~/Downloads/mybootstrap.tar.bz2 -t core,audio,cli-extra`

*When prompted create a username and password.*

#### Enter Crouton.
`sudo enter-chroot -n bionic`

#### Install some basic software while in crouton and then exit.
`sudo apt install xterm xinit -y`
`exit`

#### Install additional targets.
`sudo crouton -n bionic -t xiwi,extension,keyboard -u`

#### Install LAMP target.

`sudo crouton -n bionic -T ~/Downloads/lamp -u`

#### Download Script to make rootfs rewriteable.(Only neccessary if you want to autostart Crouton.)

`curl -Lk --connect-timeout 60 -m 300 --retry 2 "https://gist.githubusercontent.com/DennisLfromGA/6690677/raw/817787b7a6d2ca5d8993b8d4c2311cfc2ae86ae4/rw-rootfs" -o ~/Downloads/rw-rootfs`

#### Make rootfs rewriteable. (Only neccessary if you want to autostart Crouton.)

`sudo sh ~/Downloads/rw-rootfs`

#### Autostart Crouton when Chromebook starts by copying these files into ChromeOS.

`sudo cp ~/Downloads/crouton.conf /etc/init/`

`sudo cp ~/Downloads/crouton.init /usr/local/`

#### Add Common Alias to bash file.
`sudo nano ~/.bashrc`
```
alias bionic="sudo enter-chroot -n bionic"

```

#### Backup

`sudo edit-chroot -b bionic -f ~/Downloads/`

#### Restore
`sudo edit-chroot -f ~/Downloads/ -r bionic`


