# Driving Videos

## FFmpeg Concatenate

https://trac.ffmpeg.org/wiki/Concatenate

Build file with file names to concatenate

```
find /Volumes/photos_drive/driving -name "*MP4" > driving_files.txt
```

See if all file names are uniq

```
cat driving_files.txt  | cut -d'/' -f6 |wc -l
    3346

cat driving_files.txt  | cut -d'/' -f6 | sort | uniq | wc -l
    3104
```

Get list of duplicates

```
cat driving_viles.txt  | cut -d'/' -f6 | sort | uniq -d > dupes.txt
```
Remove duplicate files

Concatenate!






