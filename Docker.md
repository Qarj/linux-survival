# Docker

## Install

https://docs.docker.com/engine/install/ubuntu/

```sh
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```

Post install instructions to not need `sudo`

```sh
sudo groupadd docker
sudo usermod -aG docker $USER
```

Reboot or re-log user.

https://docs.docker.com/engine/install/linux-postinstall/

Get docker to start on boot.

```sh
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

Check version and hello-world

```sh
docker --version
.
Docker version 20.10.12, build e91ed57
.
docker run hello-world
```

## Infos

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

## Common commands

```sh
docker build -t qarj/posts .
docker run [image id or image tag]
docker run -it qarj/posts sh
docker ps
docker exec -it [container id] [command]
docker logs [container id]
docker run -it qarj/posts sh
```

CTRL+P+Q to exit container without stopping it.
CTRL+D to exit container and stop it.

Getting logs

```sh
docker run qarj/posts
```

Then in another terminal

```sh
docker ps
docker logs [container id]
```
