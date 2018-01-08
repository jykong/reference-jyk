## Command Line Audio/Video Processing & Conversion

### Download binaries
brew install youtube-dl ffmpeg lame

### Download from Youtube
#### Audio only (best quality mp3)
youtube-dl --extract-audio --audio-quality 0 --audio-format mp3 https://youtu.be/share_url

https://github.com/rg3/youtube-dl/blob/master/README.md#post-processing-options

### Convert audio formats (to best quality mp3)
ffmpeg -i input.opus -codec:a libmp3lame -qscale:a 0 output.mp3

https://trac.ffmpeg.org/wiki/Encode/MP3

### Compress video (ffmpeg defaults)
ffmpeg -i input.mp4 output.mp4
