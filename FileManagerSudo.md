# Desktop shortcut to open File Manager as root

Tested with:
- Ubuntu 16.04, Ubuntu 18.04

Open new terminal (CTRL-ALT T) then:
```
sudo apt install lxqt-sudo
gedit Desktop/sudomanager.desktop
```

Copy paste:
```
[Desktop Entry]
Name=Sudo Manager
Exec=lxqt-sudo nautilus
Type=Application
Icon=system-file-manager
```

Save close then:
```
chmod +x Desktop/sudomanager.desktop
```

