# Pirate Radio

simple command-line radio station

## usage

`pirr [options] [mplayer options]`

## examples

Broadcast the playlist hotline.m3u, shuffled:
``` sh
pirr -sbl hotline
```

Listen to that broadcast from another computer, with extra bass:
``` sh
pirr -e boom http://10.0.1.12:8000/radio
```

Change playlists on a live broadcast
``` sh
pirr -f fadeout -l newplaylist
```

## options

In any mode:

- `-s` - shuffle a playlist. Used only with `-l`, and is forgotten upon
	subsequent calls with `-l`, unless `-s` is included again.
- `-l <playlist>` - load a playlist. If a broadcast is active, the playlist
	is loaded in the broadcast.
- `-e [<preset or EQ>>]` - set equalizer to a preset or literal value, in the
	same format as [mplayer's `equalizer` audio filter](http://www.mplayerhq.hu/DOCS/man/en/mplayer.1.html#AUDIO FILTERS).

	presets:
	- `boom` - `2:8:0:0:0:0:0:0:0:0` (boost the 31.25-62.5 Hz range,  big buttery bass)
- `-f ` - force past warnings (e.g. quitting daemons)

Only when starting:

- `-b` - broadcast to icecast on the port set in `.service/icecast.xml`
- `-S` - make the broadcast sticky, so that it doesn't die when mplayer stops; use with `-b`
- `-v` - verbose output

Only while a broadcast is active:

- `-n` - skip to the next track in the playlist
- `-p` - skip to the previous track in the playlist
- `-a` - appends the loading playlist to the one already playing; used with `-l`
- `-k` - stop a broadcast
- `-q` - quiet: suppress all output to stdout
- `-c` - pass an input command to mplayer (e.g. `pause` or `loadfile /home/me/music/lovely.mp3`)
- `-x` - apply an effect before (must be the first option) or after any other command.
	- `fade` - fade volume to a new value, e.g. `-x "fade 5"`
	- `fadeout` - fade volume to 0 over 1 second
	- `fadein` - fade volume to 25 (default starting volume) over 1 second
- `-y` - pipe a spoken message into Soundflower, thus the broadcast (excludes all other options)
- `-V` - select a voice to speak in with `-y`. Pass `-V ?` for a list of voices; used with `-y`
- `-t <1-9>` - seek to a portion of the video
- `-i` - show file information

## installation

- Copy `.pirr/darkice.default.cfg` to `.pirr/darkice.cfg`, and make any changes you need.
- Copy `.pirr/icecast.default.xml` to `.pirr/icecast.xml`, and make any changes you need.
- Copy `.pirr/config.default.sh` to `.pirr/config.sh`, and make any changes you need.

### Mac

- Use [Homebrew](http://brew.sh) to install the following packages
	```
	brew install mplayer jack darkice icecast coreutils`
	```
	- `mplayer` is the media player
	- `jack` captures output from soundflower
	- `darkice` streams from jack to the radio server
	- `icecast` is the radio server
	- **optional** `coreutils` contains `gshuf`, which is needed for shuffling a dynamically loaded playlist
	- **optional** `id3lib` contains `id3info`, which shows mp3 meta information
	- **optional** `mp4v2` contains `mp4info`, which shows m4a (AAC) meta information
- Install [Soundflower](https://rogueamoeba.com/freebies/soundflower/)

## broadcast (currently Mac only)

- set soundflower 2ch to default input and output (System Preferences.app)
- run `pirr -l <playlist path> -b`
- **if** you don't want your system sounds dumping into the radio broadcast
	- set default sound input/output back to the built-in
- navigate to `http://localhost:8000/`, or whichever host/port you configured in `.service/icecast.xml`

## caveats

This tool was created for personal use on a Mac running OS X 10.9.5. No testing
has been done on other systems. I intend to make it more portable to other
POSIX systems, eventually.

## thanks

Most of the information that helped me to get the first version working, and
the idea for piping in text-to-speech, came from [this
article](http://dzello.com/blog/2012/11/21/live-stream-audio-from-osx-mountain-lion-with-icecast-and-darkice/)
by [@dzello](https://github.com/dzello).
