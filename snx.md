# snx R71

Tutorial: https://www.youtube.com/watch?v=CovvFeHImmQ

Install prerequisites

```sh
sudo dpkg --add-architecture i386
sudo apt install libpam0g:i386 libx11-6:i386 libstdc++6:i386 libstdc++5:i386 libnss3-tools
```

Set root password

```sh
sudo passwd root
```

Unlock the account

```sh
sudo passwd -u root
.
passwd: password expiry information changed.
```

Download from https://supportcenter.checkpoint.com/supportcenter/portal/user/anon/page/default.psml/media-type/html?action=portlets.DCFileAction&eventSubmit_doGetdcdetails&fileid=22824

File will be downloaded to `$HOME/Downloads/snx_install_linux30.sh`

Run script

```sh
cd $HOME/Downloads
chmod +x snx_install_linux30.sh
./snx_install_linux30.sh
.
Installation successfull
```

Revert root account - lock it again

```sh
sudo passwd -l root
```

Setup `.snxrc` file

```sh
gedit $HOME/.snxrc
```

Copy Paste

```txt
server connect.company.com
username user.name
reauth yes
debug yes
```

Connect

```sh
snx
```

Disconnect

```sh
snx -d
```

# Debugging

```sh
cat $HOME/snx.elg
```

```sh
sudo ldd /usr/bin/snx
```

# SNX 800007075

https://unix.stackexchange.com/questions/450229/getting-checkpoint-vpn-ssl-network-extender-working-in-the-command-line/453727#453727

```sh
cd $HOME/Downloads
mkdir 800007075
cd 800007075
wget https://starkers.keybase.pub/snx_install_linux30.sh?dl=1 -O snx_install.sh
sudo dpkg --add-architecture i386
sudo apt install libstdc++5:i386 libx11-6:i386 libpam0g:i386
chmod a+rx snx_install.sh
sudo ./snx_install.sh`
```

Check for missing libraries

```sh
sudo ldd /usr/bin/snx
```

Do initial connect

```sh
snx -s connect.company.com -u user.name
```

Check signature

```sh
cat /etc/snx/USER.db
```

# strongswan

https://docs.strongswan.org/strongswan-docs/5.9/install/install.html

https://community.checkpoint.com/t5/Remote-Access-VPN/3rd-party-or-OpenVPN-client-and-Check-Point-RA/td-p/48864
