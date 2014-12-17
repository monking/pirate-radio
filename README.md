# Pirate Radio

The `play` script gives you some tools to play this stuff how you want it:

## usage

`./play [playlist] [options] [mplayer options]`

## options

- `-eq-boom` - boost the 31.25-62.5 Hz range (big buttery bass)
- `-no-shuffle` - play the playlist in order
- `-enable-video` - if a file in a playlist has audio, this will allow it to show

Any other options will be passed directly to `mplayer`.

## broadcast

- set soundflower 2ch to default input and output (System Preferences.app)
- run `./play playlist -broadcast`
- **if** you don't want your system sounds dumping into the radio broadcast
	- set default sound input/output back to the built-in

## examples

`./play hotline -eq-boom -volume 6`

## installation

### Mac

- do `brew install mplayer jack darkice icecast` in the command line
- install [soundflower](https://rogueamoeba.com/freebies/soundflower/)
