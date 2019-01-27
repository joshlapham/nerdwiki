# Raspberry Pi 1 & 2

## 720p video

Using [Raspbian](https://www.raspbian.org/).

Edit `/boot/config.txt` to add: `gpu_mem=64`

## Video

### Start playing video from CLI

`omxplayer -o hdmi nameoffile.mkv`

# Other

## PiVPN & pi-hole

- http://www.pivpn.io/
- https://pi-hole.net/

### Ad Blocking When Using VPN

- https://github.com/pivpn/pivpn/issues/66
- https://github.com/pivpn/pivpn/wiki/FAQ#installing-with-pi-hole

Edit `/etc/dnsmasq.conf`:

`listen-address=127.0.0.1, 192.168.1.88, 10.8.0.1`

### Adding Routes

Default install has IP range of `10.8.0.0`, but our internal network might be a diffrent range. Edit `/etc/openvpn/server.conf`:

`push "route 192.168.1.0 255.255.255.0"`

## Shairport

Instructions 'borrowed' from [this blog post](http://www.raspberry-pi-geek.com/Archive/2015/09/Using-the-Raspberry-Pi-as-an-AirPlay-server).

Tested on Raspberry Pi 2 running Raspbian Debian 'Jessie'.

Run script to install:

```bash
#!/bin/bash

sudo apt update
sudo apt upgrade
sudo apt -y install libssl-dev libavahi-client-dev libasound2-dev avahi-daemon

cd /tmp
git clone https://github.com/abrasive/shairport.git
cd shairport
./configure
make
sudo make install

sudo cp scripts/debian/init.d/shairport /etc/init.d/
sudo cp scripts/debian/default/shairport /etc/default/
```

Edit config file: `sudo nano /etc/default/shairport`

```
# User and group under which shairport should be run
# user should have permission to output sound
# Check the audio output documentation for details.
USER=pi
GROUP=nogroup
...
# Set the AirPlay advertised name.
# Defaults to computer's hostname
AP_NAME=Raspberry Pi
...
# Force the mDNS backend
# By default, shairport will try all backends until one works.
# Check 'shairport -h' for details
MDNS=avahi
```

Test and start as service:

```bash
shairport -a 'Shairport Test'
sudo update-rc.d shairport defaults
sudo service shairport start
```

May also need to adjust sound volume: `alsamixer`
