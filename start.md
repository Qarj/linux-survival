# start

Start cmd as a detached process

```
sudo gedit /usr/local/bin/start
```

Copy Paste

```bash
#!/bin/bash

# just start a gnome-terminal if no arguments
if [ $# -eq 0 ]
  then gnome-terminal
fi

if [ "$EUID" -ne 0 ]
  then echo "Not running as SUDO !!!"
fi

echo ""
echo nohup $* \> /dev/null 2\>\&1 \&
echo ""

nohup $* > /dev/null 2>&1 &
exit 0
```

```
sudo chmod +x /usr/local/bin/start
```
