# git

## Setup new host

```
git config --global user.email "tim@gmail.com"
git config --global user.name "Tim Buckland"
git config --global http.postBuffer 1048576000
git config --global credential.helper manager-core --replace-all
git config --global core.autocrlf false
git config --global core.ignorecase false
git config --global diff.tool meld
git config --global core.filemode false
git config --global core.editor "code --wait"
git config --global mergetool.keepBackup false
git config --global alias.alias "! git config --get-regexp ^alias\. | sed -e s/^alias\.// -e s/\ /\ =\ /" --replace-all
git config --global alias.changes "diff --name-status" --replace-all
git config --global alias.files "diff-tree --no-commit-id --name-only -r" --replace-all
git config --global alias.lg "log --oneline --all --graph" --replace-all
git config --global alias.localb "branch -vv" --replace-all
git config --global alias.meld "difftool -d" --replace-all
git config --global alias.removelast "reset --mixed HEAD~1" --replace-all
git config --global alias.remoteb "branch -r" --replace-all
git config --global alias.summary "shortlog -n -s -e" --replace-all
git config --global alias.pruneremote "remote prune origin" --replace-all
git config --global alias.unstage "restore --staged" --replace-all
git config --global alias.unstageall "restore --staged ." --replace-all
```

```
git config credential.helper
.
manager-core
```

```
git credential-manager version
```

Maybe deprecated

```
git config --global credential.helper store
```

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

## Show lots of cloned repo info

```
git remote show origin
```

## Get git repo name

```
basename `git rev-parse --show-toplevel`
repo_name=$(basename `git rev-parse --show-toplevel`)
```

# Get branch name

```
git rev-parse --abbrev-ref HEAD
branch_name=$(git rev-parse --abbrev-ref HEAD)
```

# Show lots of SSH debug information

```
export GIT_SSH_COMMAND="ssh -vv"
```
