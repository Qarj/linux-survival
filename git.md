# git

## Setup new host

```
git config --global http.postBuffer 1048576000
git config --global user.email "tim@gmail.com"
git config --global user.name "Tim Buckland"
git config --global credential.helper store
git config --global core.autocrlf false
git config --global diff.tool meld
git config --global core.filemode false
git config --global core.editor "code --wait"
git config --global alias.lg "log --oneline --all"
git config --global alias.summary "shortlog -n -s -e"
```

The last one turns off treating a permissions change as change.

## See changes between latest and previous commit

```
git difftool -d HEAD^ HEAD
```

## See changes between commits to my current branch and master

```
git difftool -d master
```

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

## Stop tracking a checked-in file

```
git update-index --skip-worktree video.mp4
```
