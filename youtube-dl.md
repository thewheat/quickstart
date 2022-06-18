# Quick start for youtube-dl
- https://github.com/ytdl-org/youtube-dl/

## Default usage
youtube-dl URL

## Download certain resolution
youtube-dl -f "best[height<=480]" URL

## Download certain extension
youtube-dl -f "best[ext=mp4]" URL

## Download certain resolution & extension
youtube-dl -f "best[height<=480][ext=mp4]" URL

## Download audio only
youtube-dl -f "bestaudio" URL
youtube-dl -f "bestaudio[ext=m4a]" URL

## Download video only
youtube-dl -f "bestvideo" URL
youtube-dl -f "bestaudio[ext=mp4]" URL
youtube-dl -f "bestaudio[ext=mp4][height<=360]" URL

## Download separate video and output and combine (requires ffmpeg or avconv)
youtube-dl -f "bestvideo+bestaudio" --merge-output-format "mp4" URL

## Fallback to other formats if not found
youtube-dl -f "bestvideo[ext=mp4]+bestvideo[ext=mp3]/bestvideo[ext=mp4]+bestvideo[ext=m4a]" --merge-output-format "mp4" URL

## See all formats available
youtube-dl -F URL 

## Download specific format
youtube-dl -f format_ID URL 

## General help 
youtube-dl --help