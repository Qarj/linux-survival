# git

## Setup new host

```
git config --global http.postBuffer 1048576000
git config --global user.email "tim@gmail.com"
git config --global user.name "Tim Buckland"
git config --global credential.helper store
git config --global core.autocrlf false
git config --global core.filemode false
```

The last one turns off treating a permissions change as change.

## Prune local branches not on remote

```
git remote prune origin
```

## CentOs

```
su -
gpasswd -a test wheel
usermod -aG wheel test
su - test
sudo yum install git
```

## Preview Markdown of README.md

```
pip install grip
cd repo
grip
```
