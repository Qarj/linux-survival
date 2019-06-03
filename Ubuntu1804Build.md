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

## VirtualBox 6.0

https://tecadmin.net/install-virtualbox-on-ubuntu-18-04/

```
sudo apt update
sudo apt upgrade
```

```
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
```

```
sudo add-apt-repository "deb http://download.virtualbox.org/virtualbox/debian bionic contrib"
```

```
sudo apt install virtualbox-6.0
```

```
virtualbox
```

https://www.itzgeek.com/how-tos/mini-howtos/how-to-install-virtualbox-extension.html

```
cd /tmp
wget https://download.virtualbox.org/virtualbox/6.0.0/Oracle_VM_VirtualBox_Extension_Pack-6.0.0.vbox-extpack
```

```
File/Preferences/Extensions
```
Then browse to downloaded file in `/tmp`

## VMWare Workstation Player

https://linuxize.com/post/how-to-install-vmware-workstation-player-on-ubuntu-18-04/

CTRL-ALT-T
```
sudo apt install build-essential
sudo apt install linux-headers-$(uname -r)
wget https://www.vmware.com/go/getplayer-linux
chmod +x getplayer-linux
sudo ./getplayer-linux
```

Probably should not install as sudo...
```
sudo chown -R $USER:$USER ~/.vmware
```

## Increase SWAP file size to 8GB

https://bogdancornianu.com/change-swap-size-in-ubuntu/


```
sudo swapoff -a
sudo dd if=/dev/zero of=/swapfile bs=1G count=8
sudo mkswap /swapfile
sudo swapon /swapfile
grep SwapTotal /proc/meminfo
```

## Dropbox

```
sudo apt-get install python3-gpg
```

Sign into the Dropbox from the website in Chrome.

Then select Install, then open the `.deb` file.
Will need to restart Nautilus.

## Opera

https://vitux.com/how-to-install-uninstall-opera-browser-on-ubuntu/

```
wget -qO- https://deb.opera.com/archive.key | sudo apt-key add -
sudo add-apt-repository "deb [arch=i386,amd64] https://deb.opera.com/opera-stable/ stable non-free"
sudo apt install opera-stable
```

## Configure mouse buttons

https://askubuntu.com/questions/152297/how-to-configure-extra-buttons-in-logitech-mouse

```
sudo apt-get install xbindkeys xautomation x11-utils
```

```
xev
```

Forward arrow - button 9
```
ButtonRelease event, serial 37, synthetic NO, window 0x1800001,
    root 0x1e8, subw 0x1800002, time 7104012, (16,45), root:(318,134),
    state 0x0, button 9, same_screen YES
```

Backward arrow - button 8
```
ButtonRelease event, serial 37, synthetic NO, window 0x1800001,
    root 0x1e8, subw 0x1800002, time 7192536, (30,44), root:(332,133),
    state 0x0, button 8, same_screen YES
```

More bind examples:
- https://medium.com/@Aenon/bind-mouse-buttons-to-keys-or-scripts-under-linux-with-xbindkeys-and-xvkbd-7e6e6fcf4cba
- http://xahlee.info/linux/linux_xvkbd_tutorial.html

Forward
```
Toggle Left Click

Left Button Down
Left Button Up
wait 97 ms
Repeat until pressed again
```

Backward
```
Mega Left Click

Left Button Down
Left Button Up
wait 25 ms
Repeat while pressed
```

## Canon P-208II Scanner

Linux 32-bit driver appears to work

https://www.canon-europe.com/support/consumer_products/products/scanners/others/imageformula_p-208ii.html?type=drivers&driverdetailid=tcm:13-1238891&os=linux&language=en

Check out: http://gscan2pdf.sourceforge.net/

## Wine

```
winecfg
wine cmd.exe
```

## Archive Manager (rebranded File Roller?)

Seems to work fine.

## Install TSM

```
wine cmd.exe
cd Z:\media\sea_pro\Install\TSM
setup.exe
```

Set WOW location
```
/media/windows/Users/Public/Games/FakeWarcarft/World of Warcraft/
```

Start on boot
```
nano ~/.config/autostart/tsm.deskop
```

Copy Paste
```
[Desktop Entry]
Name=TradeSkillMaster Desktop App
GenericName=TSM Updater
Comment=Update data
Exec=wine 'C:\\Program Files (x86)\\TradeSkillMaster Application\\app\\TSMApplication.exe'
Terminal=false
Type=Application
Icon=774F_TSMApplication.0
StartupNotify=false
```


## Update TSM each hour

```
cd ~/git
git clone https://bitbucket.org/Qarj/addons
cd addons/TSM4
chmod +x AppData.lua_updater.sh
```

```
crontab -e
```

Copy Paste
```
22      *       *       *               *   /home/tim/git/addons/TSM4/AppData.lua_updater.sh
```
