# git

## Setup new host

```sh
git config --global user.email "tim@gmail.com"
git config --global user.name "Tim Buckland"
git config --global http.postBuffer 1048576000
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
git config --global pull.rebase false
```

```sh
git config credential.helper
.
manager-core
```

Or on macOS

```sh
git config credential.helper
.
osxkeychain
```

```sh
git credential-manager version
```

Linux

```sh
git config --global credential.helper store
```

Windows

```
git config --global credential.helper manager-core --replace-all
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

## Undo last commit that has not been pushed upstream

This will remove the local commit and unstage the changes.

```sh
git reset HEAD~
```

## Force git to recognise file or folder case changes e.g example -> Example

```sh
git rm -r --cached .
git add --all .
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

```sh
git update-index --skip-worktree video.mp4
```

## Show lots of cloned repo info

```sh
git remote show origin
```

## Get git repo name

```sh
basename `git rev-parse --show-toplevel`
repo_name=$(basename `git rev-parse --show-toplevel`)
```

# Get branch name

```sh
git rev-parse --abbrev-ref HEAD
branch_name=$(git rev-parse --abbrev-ref HEAD)
```

# Show lots of SSH debug information

```sh
export GIT_SSH_COMMAND="ssh -vv"
```

## Take master version of conflicted file after git pull origin master

```sh
git checkout --theirs -- path/to/conflicted_file.ext
git add path/to/conflicted_file.ext
```
