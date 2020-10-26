# UK Keyboard

cd /etc/xrdp/
sudo wget http://c-nergy.be/downloads/km-0809.ini
sudo xrdp -kill
sudo xrdp

might need to 
```
sudo apt install lxde lxde-common
```

then

```
nano /etc/xrdp/startwm.sh
```

and change to use `startlxde` instead of `startxfce` (depending on x window manager)

# Tab autocomplete fix for XFCE

https://askubuntu.com/questions/517270/fix-for-xubuntu-xrdp-tab-autocomplete-in-multi-user-environment
