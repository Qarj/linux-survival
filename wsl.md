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
