# VirtualBox Guest Additions

## Ubuntu 16.04, Ubuntu 18.04, Ubuntu 18.10

CTRL-ALT-T:
```
sudo apt install linux-headers-$(uname -r) build-essential dkms
```

Then insert the image, click `Run`.

Restart.

## Debian 9

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

In the `/dev/sr0/` row change `user,noauto` to `user,noauto,exec`. Save, close.

Then insert the image, click `Run`.

Restart.

## CentOS 7

ALT-F2 -> `gnome-control-center` -> type `keyboard` in search -> Keyboard

Scroll to bottom, click `+`

Name `Terminal`
Command `gnome-terminal`
Set Shortcut... -> CTRL-ALT-T
Click `Add`

CTRL-ALT-T: (if network is disabled on boot)
```
su -
cd /etc/sysconfig/network-scripts/
sed -i -e 's@^ONBOOT=no@ONBOOT=yes@' ifcfg-enp0s3
```
Might be called `ifcfg-eth0`.

```
su -
yum update kernel*
reboot
```

CTRL-ALT-T:
```
su -
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install kernel-devel kernel-headers dkms gcc make bzip2 perl
KERN_DIR=/usr/src/kernels/`uname -r`/build
export KERN_DIR
```

Then insert the image, click `Run`.

```
reboot
```
