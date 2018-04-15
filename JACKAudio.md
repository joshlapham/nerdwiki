# JACK Audio

## Setup

Tested on Ubuntu 16.04

```bash
sudo apt install pulseaudio-module-jack
sudo apt install qjackctl

sudo pactl load-module module-jack-sink
sudo pactl load-module module-jack-source
```

### Troubleshooting

`pulseaudio` can sometimes cause issues and need to restart it: `pulseaudio -k`

## Apps

```bash
sudo apt install calf-plugins
sudo apt install rosegarden
sudo apt install hydrogen
sudo apt install jack-keyboard
sudo apt install guitarix
```
