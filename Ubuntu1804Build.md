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

### Notes

The printer is listed 2 times in Chrome. The correct one is
- HP-LaserJet-Professional-P1102w

https://askubuntu.com/questions/1070450/hplip-hp-device-manager-print-job-has-completed-but-nothing-happens-hp-la

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

## Patch VMWare Workstation Player

```
cd /media/pro/VMs/macOS 10.14/Patch Tool/unlocker210
sudo bash ./lnx-install.sh
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

Saved Variables location
```
/media/windows/Users/Public/Games/World of Warcraft/_retail_/WTF/Account/WINBER/SavedVariables/
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

## Install Twitch - what a piece of junk!

https://www.twitch.tv/downloads

Download TwitchSetup.exe

Copy to wow prefix
```
cp ~/Downloads/TwitchSetup.exe ~/Games/world-of-warcraft/drive_c/users/Public/
```

Start installer
```
WINEPREFIX=~/Games/world-of-warcraft wine $HOME'/Games/world-of-warcraft/drive_c/users/Public/TwitchSetup.exe'
WINEPREFIX=~/Games/world-of-warcraft wine $HOME'/Games/world-of-warcraft/drive_c/users/tim/Application Data/Twitch/Bin/CurseClientUpdater.exe'
WINEPREFIX=~/Games/world-of-warcraft wine $HOME'/Games/world-of-warcraft/drive_c/users/tim/Application Data/Twitch/Bin/Twitch.exe'
WINEPREFIX=~/Games/world-of-warcraft wine $HOME'/Games/world-of-warcraft/drive_c/users/tim/Application Data/Twitch/Bin/UninstallTwitch.exe'
```

```
WINEPREFIX=~/Games/world-of-warcraft wine $HOME'/Games/world-of-warcraft/drive_c/users/tim/Application Data/Twitch/Bin/UninstallTwitch.exe'
```

## Instal WowMatrix instead

Download it anywhere and it can be started without installing
```
WINEPREFIX=~/Games/world-of-warcraft wine $HOME'/Games/world-of-warcraft/drive_c/users/Public/Public/WowMatrix.exe'
```

## Setup Radio Stations

Rhythm Box - Click `Add` min menu bar

Bayern 2
http://streams.br.de/bayern2nord_2.m3u


## Langenscheidt

Install Version 4.0, Revision 20.1
https://www.langenscheidt.com/kundenservice/updates-und-patches

The version inside the DAF folder is the right one.

code ~/Desktop/eDict.desktop
```
[Desktop Entry]
Name=eDict
Exec=env WINEPREFIX="/home/tim/.wine" wine start /unix /home/tim/.wine/dosdevices/c:/Program\ Files\ \(x86\)/Langenscheidt/e-Dictionaries/eW_lkg.exe
Type=Application
StartupNotify=true
Path=/home/tim/.wine/dosdevices/c:/Program Files (x86)/Langenscheidt/e-Dictionaries
Icon=38F3_ew_lkg.0
StartupWMClass=eW_lkg.exe
```

Path to determine icon location - look at the .desktop files
```
/home/tim/.local/share/applications/wine/Programs/Langenscheidt e-Dictionaries
```


## Monitor blanking

Dell U2711 monitor does not go off when power save mode entered
```
xset dpms force off
```
https://unix.stackexchange.com/questions/42203/turning-off-dual-monitors-with-xset-dpms-force-off-does-not-work-why

## CPU Monitor

```
sudo apt install htop
htop
```

## Minimise to dock

```
gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'
```

Then restore default behaviour since it is annoying
```
gsettings reset org.gnome.shell.extensions.dash-to-dock click-action
```

## Network monitor
http://localhost:2605/index.html

http://codebox.org.uk/pages/bitmeteros-downloads
https://github.com/codebox

Download and double click on .deb file.

https://codebox.net/pages/bitmeteros-faq

```
chromium-browser --app=http://localhost:2605/index.html
```

Create desktop shortcut

```
which chromium-browser
```

code ~/Desktop/BitMeter.desktop
```
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Type=Application
Terminal=false
Exec=/usr/bin/chromium-browser --app=http://localhost:2605/index.html
Name=BitMeter
Comment=BitMeter OS
Icon=none
```

Make it trustable
```
chmod 777 ~/Desktop/BitMeter.desktop
```


## BitMeter Python 2 Client

Accept MS Eula by using TAB key then enter
```
sudo apt install make gcc libgtk-3-dev libwebkitgtk-dev libwebkitgtk-3.0-dev libgstreamer-gl1.0-0 freeglut3 freeglut3-dev python-gst-1.0 python3-gst-1.0 libglib2.0-dev ubuntu-restricted-extras libgstreamer-plugins-base1.0-dev
```

Takes 5+ mins, installed version 4.0.6 - June 2019
```
sudo pip install wxpython
```

```
git clone https://github.com/codebox/bitmeteros-python-client.git
```

https://askubuntu.com/questions/1073145/how-to-install-wxpython-4-ubuntu-18-04

To accept MS Eula:
https://askubuntu.com/questions/16225/how-can-i-accept-the-microsoft-eula-agreement-for-ttf-mscorefonts-installer


## Install Chromium

```
sudo apt install chromium-browser
```


## Take Snip

Select snip area
```
SHIFT + Print Screen
```

## G502 Mouse

Slow down acceleration
https://www.reddit.com/r/linux_gaming/comments/9hqzib/logitech_g502_on_linux/


## Enable esync

https://github.com/lutris/lutris/wiki/How-to:-Esync

```
ulimit -Hn
```

Should be >= 524288

```
sudo nano /etc/systemd/system.conf
sudo nano /etc/systemd/user.conf
```

add
```
DefaultLimitNOFILE=524288
```

## Irfanview

Irfanview when installed in Windows is portable, there is no need to install it in wine.

However to associate with files will require the Linux path to be converted to a Windows path
with a script.

```
gedit ~/.wine/Irfan
```

Copy Paste
```
 #!/bin/sh

WINEPROGRAM="/media/windows/Program Files (x86)/IrfanView/i_view32.exe"
PROGRAMPARM=`winepath -w "$*"`
wine start /unix "$WINEPROGRAM" "$PROGRAMPARM"
exit 0
```

```
chmod +x ~/.wine/Irfan
```

Now add the .desktop file so the script appears in the list of known applications
```
sudo gedit /usr/share/applications/Irfan.desktop
```

Copy Paste
```
[Desktop Entry]
Name=Irfanview
GenericName=Irfanview
Comment=Irfan Image Viewer
Exec=/home/tim/.wine/Irfan %f
Terminal=false
Type=Application
Icon=/home/tim/.local/share/icons/hicolor/256x256/apps/IrfanView.png
StartupNotify=false
```

The 256x256 `IrfanView.png` icon can easily be found on the internet, just download it
as an icon in your home folder.

/home/tim/.local/share/icons/hicolor/256x256/apps/IrfanView.png

## Support exFAT USB

```
sudo apt install exfat-fuse exfat-utils
```

## Setup Vivald browser

https://vivaldi.com/

Download and double click on the `.deb` file

## Keyboard shortcuts

Settings / Devices / Keyboard / Launchers

Assign home folder to `Super + E`
Assign command `gnome-system-monitor` to `CTRL-SHIFT-ESC`

## Disable ipv6 on boot
https://itsfoss.com/disable-ipv6-ubuntu-linux/

```
sudo gedit /etc/sysctl.conf
```

Add lines to end
```
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1
```

Activate
```
sudo sysctl -p
```

Check
```
ip a
```

## Install 7-Zip

```
sudo apt install p7zip-full p7zip-rar
```

## Install command line tool neofetch

```
sudo apt install neofetch
```

## Install command line tool youtube-dl

```
sudo wget https://yt-dl.org/latest/youtube-dl -O /usr/local/bin/youtube-dl
sudo chmod a+x /usr/local/bin/youtube-dl
hash -r
```

```
youtube-dl <url>
```

## Install Stacer

```
sudo add-apt-repository ppa:oguzhaninan/stacer -y
sudo apt-get update
sudo apt-get install stacer -y
```

```
stacer
```

Add to CTRL-ALT-DEL by first reassigning logout to CTRL-ALT-END


## Install Sayonara music player

```
sudo apt-add-repository ppa:lucioc/sayonara
sudo apt-get update
sudo apt-get install sayonara
```

## Check temps

```
sudo apt install lm-sensors hddtemp
sudo sensors-detect
```

Check
```
sensors
```

## Install Notepadqq

```
sudo snap install --classic notepadqq
```

```
notepadqq
```

## Brave browser
https://brave-browser.readthedocs.io/en/latest/installing-brave.html#linux

```
curl -s https://brave-browser-apt-release.s3.brave.com/brave-core.asc | sudo apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add -

source /etc/os-release

echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ $UBUNTU_CODENAME main" | sudo tee /etc/apt/sources.list.d/brave-browser-release-${UBUNTU_CODENAME}.list

sudo apt update

sudo apt install brave-keyring brave-browser
```

## Install Insync for OneDrive and Google Drive

https://www.insynchq.com/3


## Install Notepad++

Install from Ubuntu Software.

Now make a script to launch from the command line.

```
sudo gedit /usr/local/bin/npp
```

Copy Paste
```
 #!/bin/sh

/snap/bin/notepad-plus-plus "$*"
exit 0
```

```
sudo chmod +x /usr/local/bin/npp
```


## Easy Find
Find across all folders except /media

```
sudo gedit /usr/local/bin/efind
```

Copy Paste
```
#!/bin/bash
if [ "$EUID" -ne 0 ]
  then echo "Not running as SUDO !!!"
fi

echo ""
echo find / -path /media -prune -o -name "$1" -print 2\>\&1 \| grep -v "Permission denied"
echo ""

find / -path /media -prune -o -name "$1" -print 2>&1 | grep -v "Permission denied"
exit 0
```

```
sudo chmod +x /usr/local/bin/efind
```

```
efind README.md
```

## Global Find
Find across all folders including /media

```
sudo gedit /usr/local/bin/gfind
```

Copy Paste
```
#!/bin/bash
if [ "$EUID" -ne 0 ]
  then echo "Not running as SUDO !!!"
fi

echo ""
echo find / -name "$1" 2\>\&1 \| grep -v "Permission denied"
echo ""

find / -name "$1" 2>&1 | grep -v "Permission denied"
exit 0
```

```
sudo chmod +x /usr/local/bin/gfind
```

```
gfind notepad++.exe
```

## Install Skype

`.deb` file seems to work

## Install UltraEdit

Start from command line
```
sudo uex README.md
```

Make a script to start as a detached process
```
sudo gedit /usr/local/bin/ue
```

Copy Paste
```
#!/bin/bash
if [ "$EUID" -ne 0 ]
  then echo "Not running as SUDO !!!"
fi

echo ""
echo nohup uex $* \> /dev/null 2\>\&1 \&
echo ""

nohup uex $* > /dev/null 2>&1 &
exit 0
```

```
sudo chmod +x /usr/local/bin/ue
```

## Install Handbrake

https://handbrake.fr/

https://launchpad.net/~stebbins/+archive/ubuntu/handbrake-releases
```
sudo add-apt-repository ppa:stebbins/handbrake-releases
sudo apt-get update
sudo apt-get install handbrake-gtk
sudo apt-get install handbrake-cli
```

## Install Slack

https://slack.com/intl/en-gb/downloads/linux


## Install MapSource

https://wiki.openstreetmap.org/wiki/OSM_Map_On_Garmin/WINE_MapSource


Download 6.16.3 https://www8.garmin.com/support/download_details.jsp?id=209
```
cd ~/Downloads
7z x MapSource_6163.exe
wine start MSmain.msi
wine MapSource_6163.exe
```

Quit MapSource, then install a map from https://openmtbmap.org

```
wine mtbgreat-britain.exe
```

Start MapSource again

```
wine ~/.wine/drive_c/MapSource/MapSource.exe
```

Select the map using the menus
```
View -> Switch to Product -> select the map
```

USB workaround
```
wine doesn't support usb, so you need the garmin_gps module. If it's installed on your system, it should load automatically after attaching your device and switching it on.
You should now have a device ttyUSB0, which you need to symlink as com1 for wine: ln -s /dev/ttyUSB0 ~/.wine/dosdevices/com1
Run MapSource: wine ~/.wine/drive_c/MapSource/MapSource.exe
Go to Settings -> Transfer, there you can select a serial port. Select COM1.
Click the map selection tool from the buttons and select an area.
Select Transfer -> Transfer to device. If everything went fine, it'll detect your garmin device attached to the serial port and you can start your upload.
```


## Setup Templates

.txt
.xlsx
.docx

