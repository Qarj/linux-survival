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

## zip

Need to cd to parent folder before zipping or entire source path will be added.

```
zip -r zipfile.zip folder
cd ~/git/cypress-frontend-app/
zip -r ~/git/cypress-service/cypress/fixtures/cypress-frontend-app.zip cypress
```
