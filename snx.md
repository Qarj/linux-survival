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
