# VirtualBox Guest Additions

## Ubuntu 16.04, Ubuntu 18.04

CTRL-ALT-T:
```
sudo apt install linux-headers-$(uname -r) build-essential dkms
```

Then insert the image, click `Run`.

Restart.

## Debain 9

Activities -> Settings -> Keyboard

Scroll to bottom, click `+`

Name `Terminal`
Command `gnome-terminal`
Shortcut -> click `Edit` then tap CTRL-ALT-T
Click `Add`

CTRL-ALT-T:
```
su -
apt update
apt upgrade
apt install build-essential module-assistant dkms
m-a prepare
```

Now fix the CD mount options:
```
gedit /etc/fstab
```

In the `/dev/sr0/ row change `user,noauto` to `user,noauto,exec`. Save, close.

Then insert the image, click `Run`.

Restart.
