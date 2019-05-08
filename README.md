# linux-survival
Reduce the frustration of linux administration!

### Ubuntu Screen Freeze

`ALT-F2` / `CTRL-ALT-T` -> `xkill` then close offending window

Alternative in TTY
```
CTRL-ALT-F1
pgrep chrome
kill -9 1234
CTRL-ALT-F7
```

Or from tty
```
sudo service lightdm restart
```


### Ubuntu sanity essential
```
sudo apt-get remove -y unattended-upgrades -qq
```

### [Desktop short cut to open File Manager as root](FileManagerSudo.md)

### [Text editors as root](TextEditorSudo.md)

### [VirtualBox Guest Additions](VirtualBoxGuestAdditions.md)

### [Environment Variables](EnvironmentVariables.md)

### [Build Python 3](BuildPython3.md)

### [SSL](SSL.md)

### [User Admin](UserAdmin.md)

### [Video Drivers / Tools](Video.md)

## commands

### [misc](cmd.md) ps
### [git](git.md)
### [wget](wget.md)
### [crontab](crontab.md)

