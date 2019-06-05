# linux-survival
Reduce the frustration of linux administration!

### Ubuntu Screen Freeze

`ALT-F2` / `CTRL-ALT-T` -> `xkill` then close offending window

Alternative in TTY
```
CTRL-ALT-F3
pgrep chrome
kill -9 1234
CTRL-ALT-F1
```

Or from tty
```
sudo service lightdm restart
```

### install lock

```
ps aux | grep -i apt
sudo kill -9 <pid>
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

## [Ubuntu 18.04 System Build](Ubuntu1804Build.md)