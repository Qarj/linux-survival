# linux-survival

Reduce the frustration of linux administration!

### Ubuntu Window Freeze

`ALT-F2` / `CTRL-ALT-T` -> `xkill` then close offending window

Alternative in TTY

```
CTRL-ALT-F3
pgrep chrome
kill -9 1234
CTRL-ALT-F2
```

Or from tty

```
sudo service lightdm restart
```

### GNOME GUI Freeze

Press `Right Alt` + `SysRq` + `r` to take keyboard out of raw mode.

Then hit `Ctrl` + `Alt` + `F3`, login lc

```
sudo restart gdm3           OR       sudo systemctl restart display-manager
```

`Ctrl` + `Alt` + `F2` to get back to standard GUI

### CTRL-ALT-BACKSPACE

Will kill X server.

### install lock

```
ps aux | grep -i apt
sudo kill -9 <pid>
```

### Ubuntu sanity essential

```
sudo apt-get remove -y unattended-upgrades -qq
```

### find

```
sudo find / -name "myfile"
```

### update

```
ubuntu-support-status
sudo apt update
apt list --upgradable
sudo apt upgrade
sudo apt autoremove
```

### [Desktop short cut to open File Manager as root](FileManagerSudo.md)

### [Text editors as root](TextEditorSudo.md)

### [VirtualBox Guest Additions](VirtualBoxGuestAdditions.md)

### [Environment Variables](EnvironmentVariables.md)

### [Build Python 3](BuildPython3.md)

### [SSL](SSL.md)

### [User Admin](UserAdmin.md)

### [Video Drivers / Tools](Video.md)

### [Docker](Docker.md)

### [Tomcat](Tomcat.md)

### [DNS](DNS.md)

### [Keyboard](keyboard.md)

## commands

### [misc](cmd.md) ps

### [git](git.md)

### [mvn](Maven.md)

### [start](start.md)

### [wget](wget.md)

### [crontab](crontab.md)

### [bamboo](bamboo.md)
