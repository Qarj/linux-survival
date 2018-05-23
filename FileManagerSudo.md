# Desktop shortcut to open File Manager as root

Username is test in this example.

Tested with:
- Ubuntu 18.04

CTRL-ALT T:
```
sudo apt install lxqt-sudo
gedit /home/test/Desktop/sudomanager.desktop
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
chmod +x /home/test/Desktop/sudomanager.desktop
```

