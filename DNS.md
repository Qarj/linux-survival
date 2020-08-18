# DNS

# Setting static DNS servers in Ubuntu

https://www.tecmint.com/set-permanent-dns-nameservers-in-ubuntu-debian/

Check symlink
```
ls -l /etc/resolv.conf
.
lrwxrwxrwx 1 root root 39 May  4 11:34 /etc/resolv.conf -> ../run/systemd/resolve/stub-resolv.conf
```

Check current configuration
```
# This file is managed by man:systemd-resolved(8). Do not edit.
#
# This is a dynamic resolv.conf file for connecting local clients to the
# internal DNS stub resolver of systemd-resolved. This file lists all
# configured search domains.
#
# Run "resolvectl status" to see details about the uplink DNS servers
# currently in use.
#
# Third party programs must not access this file directly, but only through the
# symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a different way,
# replace this symlink by a static file or a different symlink.
#
# See man:systemd-resolved.service(8) for details about the supported modes of
# operation for /etc/resolv.conf.

nameserver 127.0.0.53
options edns0
search mycompany.domain
```

```
sudo apt install resolvconf
```

```
sudo systemctl status resolvconf.service
.
● resolvconf.service - Nameserver information manager
     Loaded: loaded (/lib/systemd/system/resolvconf.service; enabled; vendor preset: enabled)
     Active: active (exited) since Tue 2020-08-18 16:26:22 BST; 1min 6s ago
       Docs: man:resolvconf(8)
   Main PID: 6681 (code=exited, status=0/SUCCESS)
      Tasks: 0 (limit: 9259)
     Memory: 0B
     CGroup: /system.slice/resolvconf.service

Aug 18 16:26:22 test-ubbase systemd[1]: Started Nameserver information manager.
Aug 18 16:26:22 test-ubbase resolvconf[6686]: /etc/resolvconf/update.d/libc: Warning: /etc/resolv.conf is not a symbolic link to /run/resolvconf/resolv.conf
```

```
sudo systemctl start resolvconf.service
sudo systemctl enable resolvconf.service
.
Synchronizing state of resolvconf.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable resolvconf
```

Add your nameservers
```
sudo gedit /etc/resolvconf/resolv.conf.d/head
```

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

Reboot (restart command given below didn't appear to update the DNS)
```
sudo systemctl restart resolvconf.service
```
