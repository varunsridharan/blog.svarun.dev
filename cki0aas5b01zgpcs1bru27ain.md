## Auto Organize CCTV Recordings Using Bash

In my home i am running a **NVR** (`Network Attached Video Recorder`) which captures & stores all the ***CCTV*** recordings in my storage server. but the files that is created by the recorder is not well organized and it looks something like below

```bash
2020-11-27T16-01-40.mp4
2020-11-27T16-06-18.mp4
2020-11-27T16-10-29.mp4
2020-11-27T16-14-05.mp4
2020-11-27T16-15-04.mp4
```
you can see the above file name is a actually a ***Time Stamp*** and it can be easy to identify the file when we don't have large no of files. 

It will become hard when we need to look for a specific recording for a date & time.

> So i decided to write a script which can be automated using cron to organize the files.

## How it should be organized ?
I wanted this to be quickly accessible at any cost and the folder structure that i choose is below and i am sure this is the most common structure too

```
/{year}/{month}/{date}-{short-day-name}/{hour}-{minutes}-{seconds}.mp4

Example : /2020/01/01-Wed/13-04-00.mp4
```

## Why i chose BASH ?
Mainly because i don't have to install any additional software for it & i wanted to try BASH with a real-world issue 

## Let's Create The Script
> for the purpose of this blog post my recording path will be `/mnt/cctv/cam1/`

Create a file named `organizer.sh` and `#!/bin/bash` in the first line.

First we need to find all the files & directory inside the recording folder for which we can use `*` at the end of the path which  will provide the full list of files & directory inside **cam1** folder and this should be used with `for` loop so that we can loop over all the file names.

```bash
for entry in /mnt/cctv/cam1/*; do
    echo "${entry}"
done
```

Since it lists everything inside a directory we need to make sure that we are looping just for the filenames. so its better to check if its a directory or not. using `! -d $entry` will check if the given path is not a directory

```bash
if [ ! -d $entry ]; then 
    echo "${entry} is not a directory"
fi
```

when you run the above code it will provide the full path of a file instead of just the file name which  will look like below.

```bash=
/mnt/cctv/cam1/2020-11-27T16-01-40.mp4
/mnt/cctv/cam1/2020-11-27T16-06-18.mp4
/mnt/cctv/cam1/2020-11-27T16-10-29.mp4
/mnt/cctv/cam1/2020-11-27T16-14-05.mp4
/mnt/cctv/cam1/2020-11-27T16-15-04.mp4
```

so we need to extract the file name from the path string using `basename` function in `bash`

```bash
FILE_BASE_NAME="$(basename "$entry")"
```
which set the value of `FILE_BASE_NAME` as `2020-11-27T16-01-40.mp4` instead of the full path.

Next step is to extract time stamp & file extension which can be done by split the string into 2 using `tr` function.

```bash
FILE_DATE_TIME_RAW=($(echo "$FILE_BASE_NAME" | tr "." "\n"))
```

> Using `$FILE_DATE_TIME_RAW[0]` will provide the timestamp `2020-11-27T16-01-40`
> 
> Using `$FILE_DATE_TIME_RAW[1]` will provide the file extension `mp4`

Next step is to split the timestamp into 2 since we just need to extract the `date`,`month` & `year`


```bash
FILE_DATE_TIME=($(echo ${FILE_DATE_TIME_RAW[0]} | tr "T" "\n"))
```

> Using `$FILE_DATE_TIME[0]` will provide the date stamp `2020-11-27`
> 
> Using `$FILE_DATE_TIME[1]` will provide the time stamp `16-01-40`

Next step is the convert the date stamp string into machine readable string so that we can extract `date`,`month` & `year`

Since my storage server runs on ***FREEBSD*** i will be using 

```bash
CUSTOM_FORMAT=$(echo $(date -jf "%Y-%m-%d" "${FILE_DATE}" +"%Y/%b/%d-%a" ))
```

if you are running on ***debian*** then the below code will work

```bash
CUSTOM_FORMAT=$(echo $(date +"%Y/%b/%d-%a" -d "${FILE_DATE} ${FILE_TIME}"))
```

> I am not sure why the `debian` code did not work for me in `freebsd` i am new to bash and learning every day!


The final step is to make sure the output folder is created for which we need to use `mkdir` and then copy the file to new folder

```bash
FULL_SAVE_PATH="/mnt/cctv-output/cam1/${CUSTOM_FORMAT}/${FILE_DATE_TIME[1]}.${FILE_EXT}"
mkdir -p "/mnt/cctv-output/cam1/${CUSTOM_FORMAT}/"
mv "$entry" "$FULL_SAVE_PATH"
```

And here is the full script 

```bash
#!/bin/bash

SAVE_TO_PATH="/mnt/cctv-output/cam1/"
DIR_TO_USE="/mnt/cctv/cam1/"

for entry in "${DIR_TO_USE}"/*; do
	if [ ! -d $entry ]; then 
		FILE_BASE_NAME="$(basename "$entry")"
		FILE_DATE_TIME_RAW=($(echo "$FILE_BASE_NAME" | tr "." "\n"))
		FILE_DATE_TIME=($(echo ${FILE_DATE_TIME_RAW[0]} | tr "T" "\n"))
		FILE_EXT="${FILE_DATE_TIME_RAW[1]}"
		FILE_TIME=$(echo "${FILE_DATE_TIME[1]}" | tr "-" ":" )
		FILE_DATE="${FILE_DATE_TIME[0]}"

		#CUSTOM_FORMAT=$(echo $(date +"%Y/%b/%d-%a" -d "${FILE_DATE} ${FILE_TIME}")) -- Worked In Ubuntu
		CUSTOM_FORMAT=$(echo $(date -jf "%Y-%m-%d" "${FILE_DATE}" +"%Y/%b/%d-%a" ))
		FULL_SAVE_PATH="${SAVE_TO_PATH}/${CUSTOM_FORMAT}/${FILE_DATE_TIME[1]}.${FILE_EXT}"
		
		echo "Local File : ${entry} => ${FULL_SAVE_PATH}"
		mkdir -p "${SAVE_TO_PATH}/${CUSTOM_FORMAT}/"
		mv "$entry" "$FULL_SAVE_PATH"
	fi
done
```

Thats it the script is done when you run it will auto organize the files 


```
/mnt/cctv-output/cam1/2020/11/27-Fri/16-01-40.mp4
/mnt/cctv-output/cam1/2020/11/27-Fri/16-06-18.mp4
/mnt/cctv-output/cam1/2020/11/27-Fri/16-10-29.mp4
/mnt/cctv-output/cam1/2020/11/27-Fri/16-14-05.mp4
/mnt/cctv-output/cam1/2020/11/27-Fri/16-15-04.mp4
```

---

%%[blog-footer]