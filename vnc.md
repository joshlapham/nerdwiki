## Ubuntu

See [Ubuntu documentation page](https://help.ubuntu.com/community/VNC/Servers) for more info.

### Server

```
sudo apt install x11vnc
x11vnc -storepasswd
x11vnc -auth guess -forever -loop -noxdamage -repeat -rfbauth /home/jl/.vnc/passwd -rfbport 5900 -shared
```

### Client

```
sudo apt install vncviewer
vncviewer
```

## Debian

Tested on Debian Wheezy.

Ensure `x11vnc` is installed with `aptitude install x11vnc`

Add the following line to `~/.xsessionrc` -

`x11vnc -display :0 -bg -nopw -noxdamage -forever`
