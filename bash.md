# bash

# Core example showing

- source
- defining function, calling with parameter
- setting output of shell command to variable
- referring to variable
- if statement checking exit code of previous command

Note that double square bracket is sometimes needed for if due to escaping and expansion considerations.

```sh
readonly RELEASE="1.1.1"

source utils.sh
util1 "example"

function search_item () {
    local COORDS="$(python3 search-window.py out/screenshot.png "targets/$1.png")"

    if [ $? -eq 0 ]
    then
        FOUND=1
        TARGET_NAME=$1
        PRIMARY="$(echo $COORDS | grep -Po "(?<=primary confidence )[0-9.]+")"
        echo "Found target $1 with confidence $PRIMARY"
    else
        FOUND=0
        echo "Target not found [$1]"
    fi
}

search_item "window_close"
```

# nested for loop example

- random generated between 0 and 59
- inner for loop using seq to loop from 1 to $POST_TOTAL
- breaking out of outer loop
- send F5

```sh
function post_macro {
    for i in {1..15}
    do
        echo "Post loop $i"

        EXTRA=$(( RANDOM % 60 ))
        POST_TOTAL=$((15 + $EXTRA))
        for j in $( seq 1 $POST_TOTAL )
        do
            echo "  -->  Post $j times"
            xdotool key --delay 60 --window $WIN F5
        done

        search_item "post_all_done"
        if [ $FOUND -eq 1 ]
        then
            echo "Can exit outer loop now"
            break
        fi

    done
}
```

# accessing windows

```sh
function target_window {
    # https://superuser.com/questions/142945/bash-command-to-focus-a-specific-window
    wmctrl -a "Target Window Title"
}

function window_handle {
    echo WIN="$(xdotool search --onlyvisible --name "Target Window Title")"
}

function resize_window {
    wmctrl -r "Target Window Title" -e 0,0,0,1920,1080
    sleep 0.2
}

function move_window {
    target_window
    sleep 0.1
    # double move required depending on which monitor window starts out on
    xdotool getactivewindow windowmove 4460 0
    sleep 0.1
    xdotool getactivewindow windowmove 4460 515
    sleep 0.1
}

WIN="$(xdotool search --name "Target Window Title" | head -1)"
CURRENT_WINDOW="$(xdotool getwindowfocus getwindowname)"
```

# checking number of arguments supplied to script

```sh
function util1 () {

    if [ $# -eq 0 ]
    then
        echo "Must specify at least one argument"
        exit 1
    fi

    python3 util.py $1 $2
}
```

# put latest release number in a variable

```sh
sudo wget http://chromedriver.storage.googleapis.com/LATEST_RELEASE -O LATEST_RELEASE
latest=$(cat LATEST_RELEASE)
```

# download file and unzip it

```sh
wget -N https://chromedriver.storage.googleapis.com/$latest/chromedriver_linux64.zip -O chromedriver_linux64.zip
sudo apt install unzip
unzip -o chromedriver_linux64.zip -d .
```

# arrays

```sh
DENYLIST=("rm" "ls" "cat" "crontab")
VER=$(echo $BASH_VERSION | cut -d '.' -f1)

for ITEM in "${DENYLIST[@]}"; do
    if [[ $VER == *"$ITEM"* ]]; then
        echo "Not accepted, sorry."
        exit 1
    fi
done
```

# typical environment variables

```sh
$BASH_VERSINFO      ${BASH_VERSINFO[0]:-0}
$BASH_VERSION
```
