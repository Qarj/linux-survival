# Install Node

# Ubuntu 20.04

Check latest script here: https://github.com/nvm-sh/nvm#installing-and-updating

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

Restart bash.

```
nvm ls-remote --lts
nvm install 12
.
Downloading and installing node v12.22.8...
Downloading https://nodejs.org/dist/v12.22.8/node-v12.22.8-linux-x64.tar.xz...
############################################################################################################################################## 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v12.22.8 (npm v6.14.15)
Creating default alias: default -> 12 (-> v12.22.8)
.
node --version
.
v12.22.8
```

Then add the following to the bottom of `.bashrc`

```
nvm use 14
```

Caution - version of npm will be changed, might need to reinstall it - `NPM.md`.

Some npm packages require `build-essential` to work so install it now.

```
sudo apt install build-essential
```

# Windows Install - via Choco

Open up an administrator command prompt and install Chocolatey

```batch
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

Install node.js

```
choco install nodejs --version=12.13.0
choco install nodejs --version=14.19.0

or for latest

choco install nodejs
```

Close command prompt and open another one. Then check the versions.

```
npm --version
node --version
```

Might have to reorder Windows path (check user as well as system path).

# Windows Install - NVM

This does not survive opening another command prompt, use the choco method.

https://github.com/coreybutler/nvm-windows

```
choco install nvm
```

From new command prompt

```
nvm list available
```

Must install specific version

```
nvm install 14.19.0
nvm use 14.19.0
```
