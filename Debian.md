## Home setup

Debian squeeze 6, 64-bit CD iso.

Only install OpenSSH server and essential system utilities.

## Steps once installed and rebooted into new system -

`aptitude install git git-core` and clone dotfiles.

`aptitude install screen`

`apt-get install --no-install-recommends xorg xfce4 alsa-base alsa-utils cpufrequtils gamin xdg-utils desktop-base gnome-brave-icon-theme dmz-cursor-theme`

`aptitude install terminator dolphin iceweasel rhythmbox`

Comment out CD-ROM from apt sources list, and add Multimedia repo -

`nano /etc/apt/sources.list`

Add `deb http://www.debian-multimedia.org stable main non-free`

Install screensavers -

`aptitude install xscreensaver-gl xscreensaver-gl-extra xscreensaver`

* Edit hostfile
* Disable IPv6
* Install NVidia
* Install smbfs
* Change keyboard layout to Macintosh 

## Install PHP on Debian without Apache

Installing `php5-cgi` package before installing `php5` package allows you to install PHP5 without installing Apache. `php5-cgi` package satisfies the dependencies that Apache provides.

## HFS read/write

Need to disable journaling in MacOS on the target drive.

`sudo aptitude install hfsplus hfsutils hfsprogs`

Edit `/etc/fstab` -

`defaults,force,rw`

Make sure all userfiles have uid of 501 for Mac compatability -

`find / -uid 1000  -exec chmod 501 "{}" \`

## Firefox

Install Firefox -

Download latest 64bit from - https://ftp.mozilla.org/pub/mozilla.org/firefox/nightly/latest-trunk/

or from Exetel mirror - https://http://mirror.exetel.com.au/pub/mozilla/firefox/releases/

Untar, create a symbolic link to `firefox` in the extracted folder to `/usr/bin/firefox`

Disable IPv6 - 

Type `about:config` into the address bar. Search for `dns`, set disable IPv6 option to `TRUE`.

## Mirrors

Exetel mirror -

Add to `/etc/apt/sources.list`

    deb http://debian.mirror.exetel.com.au/debian/ squeeze main non-free contrib
    deb-src http://debian.mirror.exetel.com.au/debian/ squeeze main non-free contrib

## Change default web browser -

Change `x-www-browser` symlink to desired application in `/etc/alternatives`

## .deb Packages

List files in a .deb package -

`dpkg -c nameof.deb`

Extract .deb package but do not install -

`dpkg -x nameof.deb /path/to/extract/to`

## Perfect server setup

From howtoforge.com

Run script/puppet manifest you made, and look at the below notes and piece it together yourself, lazy!

    General type of mail configuration: <-- Internet Site
    System mail name: <-- server1.example.com
    New password for the MySQL "root" user: <-- yourrootsqlpassword
    Repeat password for the MySQL "root" user: <-- yourrootsqlpassword
    Create directories for web-based administration? <-- No
    SSL certificate required <-- Ok

We want MySQL to listen on all interfaces, not just localhost, therefore we edit `/etc/mysql/my.cnf` and comment out the line `bind-address = 127.0.0.1`

Then restart mySQL.

During the installation, the SSL certificates for IMAP-SSL and POP3-SSL are created with the hostname localhost. To change this to the correct hostname (server1.example.com in this tutorial), delete the certificates...

`rm -f /etc/courier/imapd.pem`

`rm -f /etc/courier/pop3d.pem`

Edit `/etc/courier/imapd.cnf` and `/etc/courier/popd.cnf` -

and modify the following two files; replace CN=localhost with CN=server1.example.com (you can also modify the other values, if necessary)

Then recreate the certificates -

`mkimapdcert`

`mkpop3dcert`

and restart Courier -

`/etc/init.d/courier-imap-ssl restart`

`/etc/init.d/courier-pop-ssl restart`
