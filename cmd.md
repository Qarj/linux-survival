# cmd

https://linuxconfig.org/linux-commands

## chmod

Fix permissions for project cloned to /usr/local/bin

```sh
sudo find . -type d -exec chmod a+rwx {} \;
sudo find . -type f -exec chmod a+rw {} \;
```

## lshw - disk information

sudo lshw -class disk

## ps

```sh
ps -A | grep firefox
.
  11524 ?        00:00:07 firefox
```

## pkill

```sh
pkill firefox
```

## rsync

`--list-only`

```sh
rsync --recursive --verbose '/home/tim/source_folder_name' '/home/tim/parent_folder_for_dest_folder'
```

## tar

`--strip-components` will stop high level directory creation with archive name

```sh
mkdir ~/bamboo
tar xvzf atlassian-bamboo-7.2.4.tar.gz -C ~/bamboo --strip-components=1
```

## tr translate lower case to upper case

```sh
echo PumpkinsInHere | tr '[:lower:]' '[:upper:]'
.
PUMPKINSINHERE
```

## zip

Need to cd to parent folder before zipping or entire source path will be added.

```sh
zip -r zipfile.zip folder
cd ~/git/cypress-frontend-app/
zip -r ~/git/cypress-service/cypress/fixtures/cypress-frontend-app.zip cypress
```
