# time synchroisation

```sh
timedatectl status
.
               Local time: Sat 2022-05-07 11:25:47 BST
           Universal time: Sat 2022-05-07 10:25:47 UTC
                 RTC time: Fri 2022-05-06 03:30:36
                Time zone: Europe/London (BST, +0100)
System clock synchronized: no
              NTP service: active
          RTC in local TZ: no
```

```sh
sudo apt install chrony
sudo systemctl restart chrony.service
```

Set time servers

```sh
nano /etc/chrony/chrony.conf
```

One time sync.

```sh
chronyd -q
```

```sh
chronyc sources -v
```
