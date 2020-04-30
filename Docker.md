# Docker

Give the container a name to make management easier (otherwise container name will be randomly generated), parameter position is important
```
docker run --name gday hello-world 
docker ps -a
docker rm gday
```

All containers using an image (check with `docker ps -a`) must be removed using either container id or friendly name you gave it, or randomly generated name before the image can be removed
```
docker images
docker rmi hello-world
```

## Start a bash session in a container named ubuntu

```
docker exec -it ubuntu /bin/bash
```

## Container on Ubuntu host has no internet access

https://stackoverflow.com/questions/20430371/my-docker-container-has-no-internet

Hosts config is essentially copied to virtual machine, and 127.0.0.x won't resolve anywhere
```
cat /etc/resolv.conf
```

On Ubuntu 18.04 and later a local DNS cache is used at 127.0.0.53 which obviously is no help to a container.

This file is a symlink to `/run/systemd/resolve/stub-resolv.conf`.

```
ls -l /etc/resolv.conf
```

Change it to point to the real DNS servers at `/run/systemd/resolve/resolv.conf`, then verify.

```
sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
cat /etc/resolv.conf
docker exec -it <container name> /bin/bash
cat /etc/resolv.conf
```

In addition to this, it might be necessary to go into the network settings and specify a manual IPv4 Method.