# Networking on WSL2

Based on PreetSangha's solution in https://github.com/microsoft/WSL/issues/4285

From Windows command prompt, find out the name server your company uses

```
nslookup some.internal.server
```

The first ip address in the output is the one you want.

```
sudo nano /etc/wsl.conf
```

copy paste

```
[network]
generateResolvConf = false
```

```sh
exit
wsl --shutdown
bash
sudo rm -fd /etc/resolv.conf
exit
wsl --shutdown
bash
sudo nano /etc/resolv.conf
```

copy paste

```
# manually added company nameserver
nameserver <company name server>
```

```sh
exit
wsl --shutdown
bash
ping some.company.server
```

# Changing Distros

List available distros

```
wsl -l -o
The following is a list of valid distributions that can be installed.
Install using 'wsl --install -d <Distro>'.

NAME            FRIENDLY NAME
Ubuntu          Ubuntu
Debian          Debian GNU/Linux
kali-linux      Kali Linux Rolling
openSUSE-42     openSUSE Leap 42
SLES-12         SUSE Linux Enterprise Server v12
Ubuntu-16.04    Ubuntu 16.04 LTS
Ubuntu-18.04    Ubuntu 18.04 LTS
Ubuntu-20.04    Ubuntu 20.04 LTS
```

Remove a Distro

```
wsl --unregister Ubuntu
```

Add a Distro

```
wsl --install -d Ubuntu-20.04
```

Might need to turn off compression:

```
By default the VHDs for WSL 2 distros are stored in this path: C:\Users\[user]\AppData\Local\Packages\[distro]\LocalState\[distroPackageName]
```

# xubuntu-desktop

Add `/mnt` to PRUNEPATHS in `/etc/updatedb.conf`

```
sudo nano /etc/updatedb.conf
```

```
PRUNEPATHS="/tmp /var/spool /media /var/lib/os-prober /var/lib/ceph /home/.ecryptfs /var/lib/schroot /mnt"
```

This will stop it getting stuck on mlocate when running `sudo tasksel install xubuntu-desktop` so it doesn't index the entire Windows drive.

Follow instructions at
https://medium.com/@japheth.yates/the-complete-wsl2-gui-setup-2582828f4577

Modify instructions, in `.bashrc` put

```
export DISPLAY=10.44.x.x:0.0
export LIBGL_ALWAYS_INDIRECT=1
```

Get the 10.44 address from `ipconfig` in Windows.

Then in bash

```
sudo nano /etc/sudoers.d/dbus
```

Copy paste

```
test ALL = (root) NOPASSWD: /etc/init.d/dbus
```

Restart bash shell.

Start XLaunch in Windows. Multiple Windows. Disable access control.

Gedit should work.

```
gedit
```
