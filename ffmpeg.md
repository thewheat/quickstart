# ffmpeg Quickstart
- https://ffmpeg.org/

## Extract only video from file
```
ffmpeg -i input.mov -c:v copy -an input_video.mov
```

## Extract only audio from file
```
ffmpeg -i input.mov -c:a copy -vn input_audio.aac
```

## Combine video and audio file
```
ffmpeg -i video.mov -i audio.aac -c:v copy -c:a copy video_new.mov
```

## Rotate via https://gist.github.com/ViktorNova/1dd68a2ec99781fd9adca49507c73ee2
```
ffmpeg -i input.mov -metadata:s:v rotate="-90" -codec copy output.mov
```

## Make GIF via https://superuser.com/a/556031
```
ffmpeg -ss 30 -t 3 -i input.mp4 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif
ffmpeg -i video.mov -vf "fps=6" -loop 0 output.gif
ffmpeg -i video.mov -vf "fps=6,scale=WIDTH:-1" -loop 0 output.gif
ffmpeg -i video.mov -vf "fps=6,scale=-1:HEIGHT" -loop 0 output.gif
```
- `ss`: number of seconds to skip from start
- `t`: number of seconds to convert
- `fps` frame rate
- `scale` convert video to resolution WIDTH:HEIGHT. Use `-1` for auto
-`loop`: number of times to loop. `0` = infinite looping.


## Concatenate / Combine several files into one
https://trac.ffmpeg.org/wiki/Concatenate

```
ffmpeg -f concat -safe 0 -i mylist.txt -c copy output.wav
```

- The -safe 0 above is not required if the paths are relative.
- `mylist.txt` a list of all files to concatenated in the following form (lines starting with a ## are ignored):
```
## this is a comment
file '/path/to/file1.wav'
file '/path/to/file2.wav'
file '/path/to/file3.wav'
```

### Automatically generating the input file

#### *nix / macOS
```
## with a bash for loop
for f in ./*.wav; do echo "file '$f'" >> mylist.txt; done
## or with printf
printf "file '%s'\n" ./*.wav > mylist.txt
```
#### Windows
**Command-line**
```
(for %i in (*.wav) do @echo file '%i') > mylist.txt
```

**Powershell**
```
foreach ($i in Get-ChildItem .\*.wav) {echo "file '$i'" >> mylist.txt}
```

**bat-file**
```
(for %%i in (*.wav) do @echo file '%%i') > mylist.txt
```