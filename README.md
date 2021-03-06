# Driving Videos

## FFmpeg Concatenate

https://trac.ffmpeg.org/wiki/Concatenate

#### Build file with file names to concatenate

```
find /Volumes/photos_drive/driving -name "*MP4" > driving_files.txt
```

#### See if all file names are uniq

```
cat driving_files.txt  | cut -d'/' -f6 |wc -l
    3346

cat driving_files.txt  | cut -d'/' -f6 | sort | uniq | wc -l
    3104
```

#### Get list of duplicates

```
cat driving_viles.txt  | cut -d'/' -f6 | sort | uniq -d > dupes.txt
```

#### Remove duplicate files

#### Docker freindly paths in driving file with file directive

```
cat driving_files.txt | sed -e 's/\/Volumes\/photos_drive/file \/tmp/' > driving_files_in_docker.txt
```

#### Docker check

```
# run shell to check mounts
docker run -it --entrypoint /bin/sh -v=`pwd`:/tmp/work -v/Volumes/photos_drive/driving:/tmp/driving opencoconut/ffmpeg
```

#### Concatenate!

```
docker run -v=`pwd`:/tmp/work -v/Volumes/photos_drive/driving:/tmp/driving opencoconut/ffmpeg -f concat -safe 0 -i /tmp/work/driving_files_in_docker.txt -c copy /tmp/driving/concat.mp4
```

#### Decrease frame rate

```
docker run -v=`pwd`:/tmp/work -v/Volumes/photos_drive/driving:/tmp/driving opencoconut/ffmpeg -i /tmp/driving/concat.mp4 -r 15 /tmp/driving/concat_15fps.mp4
```

#### Scale frame size
```
docker run -v=`pwd`:/tmp/work -v/Volumes/photos_drive/driving:/tmp/driving opencoconut/ffmpeg -i /tmp/driving/concat.mp4 -vf scale=960:-1 /tmp/driving/concat_960.mp4
```


#### Create music loop

```
docker run -v=`pwd`:/tmp/work -v/Volumes/photos_drive/driving:/tmp/driving opencoconut/ffmpeg -lavfi "amovie=/tmp/work/shape_of_you_loop.wav:loop=81360" /tmp/work/loop_81360.wav
```


