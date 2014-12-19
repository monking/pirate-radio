# Pirate Radio

`play` some music, and stream it to your buddies.

## usage

`./play [options] [mplayer options]`

## options

- `-s` - shuffle
- `-v` - the player hides video by default. This allows it to play
- `-e [<preset or EQ>>]` the name of a preset below, or the value
	for `mplayer -af equalizer=<EQ>`  
	presets:
	- `boom` - `2:8:0:0:0:0:0:0:0:0` (boost the 31.25-62.5 Hz range,  big buttery bass)
- `-b` - broadcast
- `-y` - pipe a spoken message into Soundflower, thus the broadcast (excludes all other options)
- `-V` - select a voice to speak in with `-y`. Pass `-V ?` for a list of voices
- `-l <playlist>`
- `-q` - fade out and stop a broadcast

## broadcast (currently Mac only)

- set soundflower 2ch to default input and output (System Preferences.app)
- run `./play -l <playlist path> -b`
- **if** you don't want your system sounds dumping into the radio broadcast
	- set default sound input/output back to the built-in

## examples

`./play -sl hotline -e boom -volume 6`
- shuffles the playlist `playlists/hotline.m3u`, with EQ preset `boom`
- `-volume 6` will be passed through to `mplayer`

## installation

### Mac

- In the command line, do `brew install mplayer jack darkice icecast`
- Install [Soundflower](https://rogueamoeba.com/freebies/soundflower/)

## caveats

This tool was created for personal use on a Mac running OS X 10.9.5. No testing
has been done on other systems. I intend to make it more portable to other
POSIX systems, eventually.

## credits

Most of the information that helped me to get this working, and the idea for
piping in text-to-speech, came from [this
article](http://dzello.com/blog/2012/11/21/live-stream-audio-from-osx-mountain-lion-with-icecast-and-darkice/)
by [@dzello](https://github.com/dzello).
