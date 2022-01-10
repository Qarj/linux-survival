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
