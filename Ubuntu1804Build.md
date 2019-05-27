# Ubuntu 18.04 System Build

## Gnome Tweaks
Install from Ubuntu Software.

http://ubuntuhandbook.org/index.php/2018/09/pin-app-shortcut-desktop-ubuntu-18-04/

Nautilus - from `Files/Preferences`, select option `Show action to create symbolic links`

## Mounting NTFS drives at boot

https://askubuntu.com/questions/769469/symlinks-to-windows-folder-breaking

Pre-reqs
```
sudo apt-get install ntfs-3g
```

To see which drives to mount
```
sudo blkid
```

```
sudo mkdir /media/windows
sudo mkdir /media/pro
sudo mkdir /media/sea_pro
sudo mkdir /media/raptor
sudo cp /etc/fstab /etc/fstab-backup
```

```
sudo gedit /etc/fstab
```
Copy-Paste at end
```
UUID=5448442B48440DE4                     /media/windows  ntfs-3g auto,user,rw      0       0
UUID=AAA02127A020FC07                     /media/pro      ntfs-3g auto,user,rw      0       0
UUID=067652C97652B8DF                     /media/sea_pro  ntfs-3g auto,user,rw      0       0
UUID=EC02614902611A3A                     /media/raptor   ntfs-3g auto,user,rw      0       0
```

Reboot.

## Printer Driver

https://askubuntu.com/questions/1058742/how-to-install-hp-printer-in-ubuntu-18-04

Uninstall
```
sudo apt-get purge hplip hplip-data hplip-doc hplip-gui hpijs-ppds \
libsane-hpaio printer-driver-hpcups printer-driver-hpijs
sudo rm -rf /usr/share/hplip/

sudo apt-get autoremove
```

Install
```
sudo apt install build-essential python3-dev libqt4-dev
sudo apt-get install python3-pyqt4
sudo apt-get install python3-pyqt5
sudo apt-get install python3-dbus.mainloop.qt
sudo apt install libcanberra-gtk-module libcanberra-gtk3-module
python3 $(which hp-doctor)
python3 $(which hp-setup)
```

Note running `hp-doctor` will give an error message about not being able to communicate with printer (even though it detects it).
Running `hp-setup` sorts it out.

