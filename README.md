# Lovejoy's Dropbox Music

The `play` script gives you some tools to play this stuff how you want it:

## usage

`./play [playlist] [options]`

## options

- `-eq-boom` - boost the 31.25-62.5 Hz range (big buttery bass)
- `-no-shuffle` - play the playlist in order
- `-enable-video` - if a file in a playlist has audio, this will allow it to show

Any other options will be passed directly to `mplayer`.

## examples

`./play hotline -eq-boom -volume 6`

## dependencies

### mplayer

- Mac [homebrew](http://brew.sh)

	`brew install mplayer`

- Ubuntu/Debian

	`apt-get install mplayer`
