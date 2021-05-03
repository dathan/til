## Collection ffmpeg screen recordings

### ffmpeg
* ffmpeg -i in.mov -s 600x400 -pix_fmt rgb24 -r 10 -f gif - | gifsicle --optimize=3 --delay=3 > out.gif
* [source](https://gist.github.com/dergachev/4627207)

