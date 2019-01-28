## ncmpc

ncmpc is a client for MPD.

### Basic controls

* `Shift-P` - pause
* `s` - stop
* `left arrow` - vol down
* `right arrow` - vol up
* `c` - clear playlist
* `a` - add to playlist
* `t` - add all to playlist
* `y` - single mode (don't play any songs after current one stops)
* `z` - random mode
* `C` - consume mode (capital C). Deletes song from playlist after playing.

## MPD

Tested on Ubuntu 16.04

Install: `sudo apt install mpd`

Edit config file: `sudo nano /etc/mpd.conf`:

```config
music_directory "/var/lib/mpd/music"
playlist_directory "/var/lib/mpd/playlists"
db_file "/var/lib/mpd/tag_cache"
log_file "/var/log/mpd/mpd.log"
pid_file "/run/mpd/pid"
state_file "/var/lib/mpd/state"
sticker_file "/var/lib/mpd/sticker.sql"

user "mpd"
#group "nogroup"

# For network
bind_to_address "localhost"

input {
 plugin "curl"
}

audio_output {
    type "alsa"
	name "My ALSA Device"
#	device "hw:0,0"	# optional
#	mixer_type "hardware"      # optional
#	mixer_device	"default"	# optional
#	mixer_control	"PCM"		# optional
#	mixer_index	"0"		# optional
}

filesystem_charset "UTF-8"
id3v1_encoding "UTF-8"
```
