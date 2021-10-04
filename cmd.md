# cmd

https://linuxconfig.org/linux-commands

## lshw - disk information

sudo lshw -class disk

## ps

ps -A | grep firefox

## pkill

pkill firefox

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
