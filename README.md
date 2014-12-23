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

- `-s` - shuffle a playlist. Used only with `-l`, and is forgotten upon
	subsequent calls with `-l`, unless `-s` is included again.
- `-v` - the player hides video by default. This allows it to play
- `-l <playlist>` - load a playlist. If a broadcast is active, the playlist
	is loaded in the broadcast.
- `-a` - used with `-l`, appends the loading playlist to the one already playing.
	is loaded in the broadcast.
- `-e [<preset or EQ>>]` - set equalizer to a preset or literal value, in the
	same format as [mplayer's `equalizer` audio filter](http://www.mplayerhq.hu/DOCS/man/en/mplayer.1.html#AUDIO FILTERS).

	presets:
	- `boom` - `2:8:0:0:0:0:0:0:0:0` (boost the 31.25-62.5 Hz range,  big buttery bass)
- `-b` - broadcast to icecast on the port set in `.service/icecast.xml`

Only when broadcasting:

- `-y` - pipe a spoken message into Soundflower, thus the broadcast (excludes all other options)
- `-V` - select a voice to speak in with `-y`. Pass `-V ?` for a list of voices.
- `-n` `-N` - skip to the next track in the playlist. `-N` for no fadeout.
- `-p` `-P` - skip to the previous track in the playlist. `-P` for no fadeout.
- `-q` `-Q` - stop a broadcast. `-Q` for no fadeout
- `-c` - pass an input command to mplayer (e.g. `pause` or `loadfile /home/me/music/lovely.mp3`)
- `-f` - apply an effect before (must be the first option) or after any other command.
	- `fade` - fade volume to a new value, e.g. `-f "fade 5"`
	- `fadeout` - fade volume to 0 over 1 second
	- `fadein` - fade volume to 25 (default starting volume) over 1 second

## installation

- Copy `.service/darkice.default.cfg` to `.service/darkice.cfg`, and make any changes you need.
- Copy `.service/icecast.default.xml` to `.service/icecast.xml`, and make any changes you need.

### Mac

- Use [Homebrew](http://brew.sh) to install the following packages
	```
	brew install mplayer jack darkice icecast coreutils`
	```
	- `mplayer` is the media player
	- `jack` captures output from soundflower
	- `darkice` streams from jack to the radio server
	- `icecast` is the radio server
	- `coreutils` contains `gshuf`, which is needed for shuffling a dynamically loaded playlist
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
