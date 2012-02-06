## Creating a new base box

From - http://vagrantup.com/docs/base_boxes.html

Based on Debian Squeeze 32-bit ISO.

Basic requirements - 

* VirtualBox Guest Additions
* SSH key-based authentication
* Ruby and RubyGems to install Chef and Puppet
* Chef and Puppet for provisioning support

Steps to create new box -

1. Create new VM in VirtualBox. Allocate 40gb dynamic disk space.
2. Allocate 384mb RAM (default setting). Can always change this later.
3. Disable audio, USB controllers, other un-needed stuff.
4. Ensure NAT is enabled.
5. Boot install disc. Use these settings -

    * Hostname: vagrant-debian-squeeze
    * Domain: vagrantup.com
    * Root pass: vagrant
    * Main user: vagrant
    * Main user pass: vagrant

6. Don't install GUI or guest additions from Debian installer.
7. Remove installation CD from apt sources in `/etc/apt/sources.list` and run `aptitude update`
8. Boot VM, login as user. Run `aptitude install sudo`
9. Run `visudo`. Change the `env_keep` line at top of file to match the below -

`Defaults  env_keep+=SSH_AUTH_SOCK`

And add the following line to allow passwordless sudo for members of the `admin` group - 

`%admin ALL=NOPASSWD: ALL`

10. Add the `admin` group with `groupadd admin`
11. Add `vagrant` user to `admin` group with `usermod -aG admin vagrant`
12. Restart sudo with `/etc/init.d/sudo restart`
13. Run `aptitude install ruby-dev rubygems puppet`
14. Run `sudo gem install chef --no-rdoc --no-ri`
15. Run `sudo apt-get install linux-headers-$(uname -r) build-essential`
16. Mount Guest Additions in GUI under Devices.
17. Run `sudo mount /dev/cdrom /media/cdrom`
18. Run `sudo sh /media/cdrom/VBoxLinuxAdditions.run` to install Guest Additions.
19. Add `UseDNS No` to `/etc/sshd_config` to speed up SSH connections.
20. Run `apt-get clean` to clear cache and free up space.
21. Under `vagrant` user, add the following key to `~/.ssh/authorized_keys` and ensure file is chmod `0600` -

    ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA6NF8iallvQVp22WDkTkyrtvp9eWW6A8YVr+kz4TjGYe7gHzIw+niNltGEFHzD8+v1I2YJ6oXevct1YeS0o9HZyN1Q9qgCgzUFtdOKLv6IedplqoPkcmF0aYet2PkEDo3MlTBckFXPITAMzF8dJSIFo9D8HfdOV0IAdx4O7PtixWKn5y2hMNG0zQPyUecp4pzC6kivAIhyfHilFR61RGL+GPXQ2MWZWFYbAGjyiYJnAmCP3NOTd0jMZEnDkbUvxhMmBYSdETk1rRgm+R4LOzFUGaHqHDLKLX+FIPKcF96hrucXzcWyLbIbEgE98OHlnVYCzRdK8jlqm8tehUc9c9WhQ== vagrant insecure public key

22. Package the new box using the VirtualBox VM name -

`vagrant package --base my_base_box`

This will make a new file named package.box

23. Add `package.box` to Vagrant - 

`vagrant box add my_box package.box`

24. Start up the new box -

`cd test_environment`

`vagrant init my_box`

`vagrant up`

`vagrant ssh`
