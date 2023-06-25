# Install Node

# Ubuntu 20.04

Check latest script here: https://github.com/nvm-sh/nvm#installing-and-updating

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```

Restart bash.

```sh
nvm ls-remote --lts
nvm install 18
.
Computing checksum with sha256sum
Checksums matched!
Now using node v18.16.1 (npm v9.5.1)
```

Then add the following to the middle of `.bashrc`, also moving up the nvm code appended to the end.

```sh
nvm use 18
```

Caution - version of npm will be changed, might need to reinstall it - `NPM.md`.

Some npm packages require `build-essential` to work so install it now.

```sh
sudo apt install build-essential
```

# Windows Install - via Choco

Open up an administrator command prompt and install Chocolatey

```batch
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

Install node.js

```sh
choco install nodejs --version=12.13.0
choco install nodejs --version=14.19.0
choco install nodejs-lts

or for latest

choco install nodejs
```

Current lts is `16.15.0` https://community.chocolatey.org/packages/nodejs-lts

Close command prompt and open another one. Then check the versions.

```sh
npm --version
node --version
```

Might have to reorder Windows path (check user as well as system path).

Finally, go to `NPM.md` and install the required NPM version.

# Windows Install - NVM - DO NOT USE, BUGGED!

This does not survive opening another command prompt, use the choco method.

https://github.com/coreybutler/nvm-windows

```
choco install nvm
```

From new command prompt

```
nvm list available
```

Must install specific version, do not do `nvm install 16`

```
nvm install 16.15.0
nvm use 16.15.0
```
