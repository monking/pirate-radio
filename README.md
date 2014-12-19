# Pirate Radio

`play` some music, and stream it to your buddies.

## usage

`./play [options] [mplayer options]`

## examples

Broadcast the playlist hotline.m3u, shuffled:

```
./play -sbl hotline
```

Listen to that broadcast from another computer, with extra bass:

```
./play -e boom http://10.0.1.12:8000/radio
```

## options

- `-s` - shuffle
- `-v` - the player hides video by default. This allows it to play
- `-l <playlist>`
- `-e [<preset or EQ>>]` the name of a preset below, or the value
	for `mplayer -af equalizer=<EQ>`  
	presets:
	- `boom` - `2:8:0:0:0:0:0:0:0:0` (boost the 31.25-62.5 Hz range,  big buttery bass)
- `-b` - broadcast to icecast on the port set in `.service/icecast.xml`

Only when broadcasting:

- `-y` - pipe a spoken message into Soundflower, thus the broadcast (excludes all other options)
- `-V` - select a voice to speak in with `-y`. Pass `-V ?` for a list of voices
- `-n` - fade out and skip to the next track in the playlist
- `-p` - fade out and skip to the previous track in the playlist
- `-q` - fade out and stop a broadcast
- `-c` - pass an input command to mplayer (e.g. `pause` or `volume 15 1`)

## installation

- Copy `.service/darkice.default.cfg` to  `.service/darkice.cfg`, and make any changes you need.
- Copy `.service/icecast.default.xml` to  `.service/icecast.xml`, and make any changes you need.

### Mac

- In the command line, do `brew install mplayer jack darkice icecast`
- Install [Soundflower](https://rogueamoeba.com/freebies/soundflower/)

## broadcast (currently Mac only)

- set soundflower 2ch to default input and output (System Preferences.app)
- run `./play -l <playlist path> -b`
- **if** you don't want your system sounds dumping into the radio broadcast
	- set default sound input/output back to the built-in
- navigate to `http://localhost:8000/`, or whichever host/port you configured in `.service/icecast.xml`

## caveats

This tool was created for personal use on a Mac running OS X 10.9.5. No testing
has been done on other systems. I intend to make it more portable to other
POSIX systems, eventually.

## credits

Most of the information that helped me to get this working, and the idea for
piping in text-to-speech, came from [this
article](http://dzello.com/blog/2012/11/21/live-stream-audio-from-osx-mountain-lion-with-icecast-and-darkice/)
by [@dzello](https://github.com/dzello).
