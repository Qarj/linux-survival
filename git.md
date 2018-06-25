# git

## Setup new host
```
git config --global user.email "tim@gmail.com"
git config --global user.name "Tim Buckland"
git config credential.helper store
git config --global core.autocrlf false
git config --global core.filemode false
```
The last one turns off treating a permissions change as change.


## Prune local branches not on remote
```
git remote prune origin
```
