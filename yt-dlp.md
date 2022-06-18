# Quick start for yt-dlp 
- https://github.com/yt-dlp/yt-dlp


## Default usage

```
yt-dlp $URL
```

## Download specific format and resolution

```
yt-dlp -f 'b[ext=mp4][height<=480]'  $URL 
yt-dlp -f 'b[ext=mp4]' -S 'height:480' $URL 
yt-dlp -f 'b[ext=mp4]' -S 'res:480' $URL  # `res` uses smallest dimension (e.g. for portrait videos)
```

## Downloadinig multiple files
- Page filterng by not live and filesize 
- Specifiies the number of videos to download and also number of videos to parse from webpage
```
yt-dlp --max-downloads $NUMBER_OF_FILES_TO_DOWNLOAD --match-filter "!is_live" --max-filesize 500m -f 'b[ext=mp4]' -S 'res:480' --playlist-end $NUMBER_OF_VIDEOS_TO_PARSE_FROM_WEBSITE $URL -P "$OUTPUT_FOLDER"
```