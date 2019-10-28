## Command Line Audio/Video Processing & Conversion

### Download from Youtube
brew install youtube-dl
#### Audio only (best quality mp3)
youtube-dl --extract-audio --audio-quality 0 --audio-format mp3 https://youtu.be/share_url

https://github.com/rg3/youtube-dl/blob/master/README.md#post-processing-options

#### Audio only (default, highest quality, non-transcode)
youtube-dl -x https://youtu.be/share_url

### Download from Soundcloud
pip install scdl
#### Audio only (best quality mp3)
scdl -l https://soundcloud.com/share_url

### Convert files
brew install ffmpeg lame
#### Convert audio formats (to best quality mp3)
ffmpeg -i input.opus -codec:a libmp3lame -qscale:a 0 output.mp3

https://trac.ffmpeg.org/wiki/Encode/MP3

#### Compress video (ffmpeg defaults)
ffmpeg -i input.mp4 output.mp4

#### Trim audio
ffmpeg -i [input_file] -ss [start_time_in_seconds] -to [end_time_in_seconds] -c:a mp3 [output_file.mp3]