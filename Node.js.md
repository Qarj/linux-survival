# Install Node

## Windows Install

Open up an administrator command prompt and install Chocolatey

```batch
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

Install node.js

```batch
choco install nodejs
```

Close command prompt and open another one. Then check the versions.

```
npm --version
node --version
```

## Ubuntu Install

```
sudo apt install curl
```

```
curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Check node and npm versions

```batch
node -v
npm -v
```
