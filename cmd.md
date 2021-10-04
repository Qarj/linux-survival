# cmd

https://linuxconfig.org/linux-commands

## lshw - disk information

sudo lshw -class disk

## ps

ps -A | grep firefox

## pkill

pkill firefox

## rsync

`--list-only`

```
rsync --recursive --verbose '/home/tim/source_folder_name' '/home/tim/parent_folder_for_dest_folder'
```

## tar

`--strip-components` will stop high level directory creation with archive name

```
mkdir ~/bamboo
tar xvzf atlassian-bamboo-7.2.4.tar.gz -C ~/bamboo --strip-components=1
```
